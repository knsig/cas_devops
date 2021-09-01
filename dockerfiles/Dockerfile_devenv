# This points to Debian version 11.0
FROM debian:bullseye

# Install wget, bzip2 and make
RUN apt-get update && apt-get install -y wget bzip2 make

# Add cpio and libncurses5
RUN apt-get install cpio libncurses5 -y

# Prepare directory for tools
ARG TOOLS_PATH=/tools
RUN mkdir ${TOOLS_PATH}
WORKDIR ${TOOLS_PATH}

# Download the ARM toolchain
RUN wget https://developer.arm.com/-/media/Files/downloads/gnu-rm/10-2020q4/gcc-arm-none-eabi-10-2020-q4-major-x86_64-linux.tar.bz2 -O gcc-arm-none-eabi.tar.bz2

# Unpack the archive to TOOLCHAIN_PATH
ARG TOOLCHAIN_PATH=${TOOLS_PATH}/gcc-arm-none-eabi
RUN mkdir ${TOOLCHAIN_PATH} && tar xjfv gcc-arm-none-eabi.tar.bz2 -C ${TOOLCHAIN_PATH} --strip-components 1

# Remove the archive and docs
RUN rm gcc-arm-none-eabi.tar.bz2 && rm -rf ${TOOLCHAIN_PATH}/share/doc

# Install cppcheck 
RUN apt-get -y install cppcheck

# Add the arm toolchain to the path
ENV PATH="${TOOLCHAIN_PATH}/bin:${PATH}"