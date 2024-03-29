# debian:buster-20201117
FROM debian@sha256:0e9c1df5dec20d9459ba6c30354a28bc5b6926444074bcf05486e9df41da3b1a

RUN apt-get update && apt-get -y install --no-install-recommends \
	gcc \
	g++ \
	gfortran \
	libopenblas-dev \
	libblas-dev \
	liblapack-dev \
	libatlas-base-dev \
	libhdf5-dev \
	libhdf5-103 \
	pkg-config \
	python3 \
	python3-dev \
	python3-pip \
	python3-setuptools \
	pybind11-dev \
	wget


#RUN python3 -m pip install wheel==0.34.2 cython==0.29.14 pybind11==2.4.3
#RUN python3 -m pip install wheel numpy==1.18.1
#RUN python3 -m pip install wheel scipy==1.4.1
#RUN python3 -m pip install wheel --no-deps h5py==2.10.0

#RUN apt-get update && apt-get -y install --no-install-recommends \
#	python3-setuptools \
#	libopenblas-base \
#	wget \
#&& rm -rf /var/lib/apt/lists/*


#WORKDIR /root
RUN python3 -m pip install gdown

RUN gdown https://drive.google.com/uc?id=11mujzVaFqa7R1_lB7q0kVPW22Ol51MPg
RUN python3 -m pip install Cython
RUN python3 -m pip install --upgrade pip
#RUN python3 -m pip install tensorflow-addons==0.10.0
RUN python3 -m pip install tensorflow-2.2.0-cp37-cp37m-linux_armv7l.whl
RUN rm *.whl



RUN apt-get update && apt-get -y install unzip
RUN apt-get install -y build-essential
RUN apt-get -y install libjpeg-dev libpng-dev libtiff-dev
RUN apt-get -y install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
RUN apt-get -y install libxvidcore-dev libx264-dev
RUN apt-get install -y python3-dev
RUN apt-get -y install libgtk2.0-dev

ENV OPENCV_VERSION=4.5.0

# building open-cv
WORKDIR /root
RUN wget https://github.com/opencv/opencv/archive/$OPENCV_VERSION.zip
RUN wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/$OPENCV_VERSION.zip
RUN unzip -o $OPENCV_VERSION.zip && unzip opencv_contrib.zip && mv opencv_contrib-$OPENCV_VERSION opencv_contrib
RUN apt-get -y install cmake
WORKDIR /root/opencv-$OPENCV_VERSION/build

RUN cmake -D ENABLE_NEON=ON  -D ENABLE_VFPV3=ON \
      -D OPENCV_ENABLE_NONFREE=ON \
      -D CMAKE_BUILD_TYPE=RELEASE \
      -D CMAKE_INSTALL_PREFIX=/usr/local \
      -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \
      -D WITH_FFMPEG=ON -D WITH_TBB=ON -D WITH_GTK=ON -D WITH_V4L=ON -D WITH_OPENGL=ON -D WITH_CUBLAS=ON -DWITH_QT=OFF \
      -DCUDA_NVCC_FLAGS="-D_FORCE_INLINES"  --prefix=/usr --extra-version='1~16.04.york0' --toolchain=hardened --libdir=/usr/lib/x86_64-linux-gnu \
      --incdir=/usr/include/x86_64-linux-gnu --arch=amd64 --enable-gpl --disable-stripping --enable-avresample --disable-filter=resample \
      --enable-avisynth --enable-gnutls --enable-ladspa --enable-libaom --enable-libass --enable-libbluray --enable-libbs2b --enable-libcaca \
      --enable-libcdio --enable-libcodec2 --enable-libflite --enable-libfontconfig --enable-libfreetype --enable-libfribidi --enable-libgme \
      --enable-libgsm --enable-libjack --enable-libmp3lame --enable-libmysofa --enable-libopenjpeg --enable-libopenmpt --enable-libopus \
      --enable-libpulse --enable-librsvg --enable-librubberband --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libspeex \
      --enable-libssh --enable-libtheora --enable-libtwolame --enable-libvidstab --enable-libvorbis --enable-libvpx --enable-libwavpack \
      --enable-libwebp --enable-libx265 --enable-libxml2 --enable-libxvid --enable-libzmq --enable-libzvbi --enable-lv2 --enable-omx \
      --enable-openal --enable-opengl --enable-sdl2 --enable-libdc1394 --enable-libdrm --enable-libiec61883 --enable-chromaprint --enable-frei0r \
      --enable-libopencv --enable-libx264 --enable-shared ..

RUN make -j4
RUN make install
RUN ldconfig

RUN pip3 install matplotlib


CMD ["tail","-f","/dev/null"]
