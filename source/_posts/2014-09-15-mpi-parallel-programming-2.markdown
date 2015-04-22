---
layout: post
title: "mpi_parallel_programming_2"
date: 2014-09-15 15:28:34 -0400
comments: true
categories: mpi cplusplus
---

###data type
- there are only these data type in the MPI
	- if you want to use struct or multi array, you need to do something else

- |MPI data type| c data type|
|-----|------|
|MPI_CHAR|signed char|
|MPI_SHORT|signed short int|
|MPI_INT|signed int|
|MPI_LONG|signed long int|
|MPI_UNSIGNED_CHAR|unsigned long int|
|MPI_UNSIGNED_SHORT|unsigned short int|
|MPI_UNSIGNED|unsigned int|
|MPI_FLOAT|float|
|MPI_DOUBLE|double|
|MPI_LONG_DOUBLE|long double|
|MPI_BYTE||
|MPI_MPI_PACKED||
<!--more-->
###about the status
- the MPI_status combine a lots of information
    - there are at least three member in the status
        - MPI_SOURCE, MPI_TAG, MPI_ERROR
- and we can get the size of the message using 
    - MPI_Get_Count(MPI_Status *status, MPI_Datatype datatype, int* count_ptr);
    
###The broadcast idea
- you can use the MPI_Bcast idea to send the message to all the other process;
    - MPI_Bcast(void *message, int count, MPI_Datatype datatype, int root, MPI_Comm comm)

###gather the data and scatter the data
- use MPI_Gather
    - MPI_Gather(void *send_data, int send_count, MPI_Datatype send_type, void* recv_data, int recv_count, MPI_Datatype recv_type, int root, MPI_Comm comm)
- use MPI_Scatter to scatter the data
    - MPI_Scatter(void *send_data, int send_count, MPI_Datatype send_type, void *recv_data, int recv_count, MPI_Datatype recv_type, int root, MPI_Comm comm);
    - MPI_Scatter split the data referenced by send_data on the process with rank root into k segment.each of which consists of send_count elements of type send_type.
    

