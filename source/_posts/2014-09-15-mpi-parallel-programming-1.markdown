---
layout: post
title: "mpi_parallel_programming_1"
date: 2014-09-15 14:19:13 -0400
comments: true
categories: mpi cplusplus
---

###difference between SIMD and MIMD
- difference kinds of computer architecture is using the Flynn to classify
	- SISD
	- SIMD
	- MISD
	- MIMD
- we only talk about the SIMD and MIMD here
	- SIMD means that one command deal with many data streams
		- most of the single core machine is SIMD machine
		- and these kinds of machine is most used in the image processing and multimedia processing.
<!--more-->
	- MIMD means that many commands deal with many data streams
		- the lastest multicore platform is a MIMD machine
		- the MIMD are asynchronous
		- 

####the multi core hardware architecture
- the multicore CPU is combine many CPU into one chip. and each CPU core has a single processor.
	- each core has it's own cache. (some other may share one cache between multi CPU)

###message passing
- There are two methods in the message passing
	- MPI_Send
		- void * buffer, int count, MPI_Datatype datatype, int destination, int tag, MPI_Comm communicator
		- e.g
			- MPI_Send(&x, 1, MPI_FLOAT, 1, 0, MPI_COMM_WORLD);
	- MPI_Recv
		- void * buffer, int count, MPI_Datatype datatype, int source, int tag, MPI_Comm communicator, MPI_Status status
		- MPI_Recv(&x, 1, MPI_FLOAT, 0, 0, MPI_COMM_WORLD, &status);

###sample program
```
#include "mpi.h"
int main(int argc, char *argv[]){
	int rank; //rank of the process
	int source; //rank of the sender
	int dest;   //rank of the receiver
	int num;    //number of the processers
	int tags;
	char messages[1000];
	MPI_Status status;

	//setting up the MPI
	MPI_init(&argc, &argv);

	//find out the rank of the curret program
	MPI_Comm_rank(MPI_COMM_WORLD, rank);

	//find out the number of the processers
	MPI_Common_Size(MPI_COMM_WORLD, &p);

	if(rank != 0){ //if the current program is not the root program
		sprintf(message, "hello from %d", rank);
		dest = 0;
		MPI_Send(message, strlen(message) + 1, MPI_CHAR, dest, tag, MPI_COMM_WORLD);
	}else{
		sprintf(message, "hello from ");
		MPI_Recv(message, 100, MPI_CHAR, source, tag, MPI_COMM_WORLD, &status);
		printf("%s\n", message);
	}
	MPI_Finalize();
}

```

###how to run the program
- for c++
	- `mpic++ -o test test.cpp`
- for c
	- `mpicc -o test test.c`
- run 
	- for m core computer
		- `mpirun -np m test`

















