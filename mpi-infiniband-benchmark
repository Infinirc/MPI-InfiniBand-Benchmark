#include <mpi.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>  

#define BUFFER_SIZE (1024 * 1024) 

int main(int argc, char** argv) {
    int rank, size;
    char* buffer;
    MPI_Status status;
    double start_time, end_time, elapsed_time = 0.0;
    int desired_seconds;

    MPI_Init(&argc, &argv);
    MPI_Comm_rank(MPI_COMM_WORLD, &rank);
    MPI_Comm_size(MPI_COMM_WORLD, &size);

    if (argc < 2) {
        if (rank == 0) {
            fprintf(stderr, "Usage: %s <desired_seconds>\n", argv[0]);
        }
        MPI_Finalize();
        return 1;
    }

    desired_seconds = atoi(argv[1]);

    if (size != 2) {
        if (rank == 0) {
            fprintf(stderr, "This program requires exactly 2 MPI tasks.\n");
        }
        MPI_Finalize();
        return 1;
    }

    buffer = (char*)malloc(BUFFER_SIZE);
    if (buffer == NULL) {
        fprintf(stderr, "Unable to allocate buffer\n");
        MPI_Finalize();
        return 1;
    }
    memset(buffer, 0, BUFFER_SIZE);

    start_time = MPI_Wtime();
    while (elapsed_time < desired_seconds) {
        if (rank == 0) {
            MPI_Send(buffer, BUFFER_SIZE, MPI_CHAR, 1, 0, MPI_COMM_WORLD);
            MPI_Recv(buffer, BUFFER_SIZE, MPI_CHAR, 1, 0, MPI_COMM_WORLD, &status);
        } else if (rank == 1) {
            MPI_Recv(buffer, BUFFER_SIZE, MPI_CHAR, 0, 0, MPI_COMM_WORLD, &status);
            MPI_Send(buffer, BUFFER_SIZE, MPI_CHAR, 0, 0, MPI_COMM_WORLD);
        }
        end_time = MPI_Wtime();
        elapsed_time = end_time - start_time;
    }

    free(buffer);
    MPI_Finalize();
    return 0;
}
