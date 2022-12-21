-----------------------
Purpose of SGXStream
-----------------------

This repository intends to provides a set of benchmarks that can be used to
measure the memory bandwidth performance of SGX EPC memory.

---------------------------------------------
Quick Start
---------------------------------------------
Note: Remember to "make clean" before switching build mode

1. Install Intel(R) Software Guard Extensions (Intel(R) SGX) SDK for Linux OS
2. Figure out the necessary parameters before testing.
   1. The highest frequency of our platform is 2.7GHz, so set `CPU_MAX_FREQ=2.7` to make the timer in enclave working;
   2. Stream array size is default to 120000000 (approximatly 2.7 GiB memory), set this value to match your requirements.

2. Make sure your environment is set:

        $ source ${sgx-sdk-install-path}/environment

3. Build the project with the prepared Makefile:
    1. Benchmark the EPC memory (hardware mode, and set PRERELEASE=1 to get compiler optimization)

            $ make SGX_PRERELEASE=1 SGX_DEBUG=1 CPU_MAX_FREQ=2.7 STREAM_ARRAY_SIZE=120000000

    2. Benchmark the normal memory (Simulation Mode, Pre-release build)

            $ make clean
            $ make SGX_MODE=SIM SGX_PRERELEASE=1 SGX_DEBUG=0 CPU_MAX_FREQ=2.7 STREAM_ARRAY_SIZE=120000000

    3. You may also need to modify `HeapMaxSize` in `Enclave/Enclave.config.xml` for larger `STREAM_ARRAY_SIZE`.
4. Execute the binary directly:

        $ ./app

