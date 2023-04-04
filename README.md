# AWS EDGE POC

This repository contains the Yolo-client and the gstreamer-server as submodules to test the transmision
of video frames between client and server and process the image, plot boxes, and generate a new output 
video.

Please make sure that each submodule is pointing to the exact commit you are intending to test

## Author: fede, peter, lau

## Installation

Must have docker and docker compose installed.

1. Build the containers from this folder by executing:

```bash
docker-compose build
```

2. Get inside yolo container by executing:

```bash
docker-compose run yolo bin/bash
```

3. Get inside gstreamer container by executing:

```bash
docker-compose run gst-container bin/bash
```

All container's shells will have an assigned ip sharing same subnetwork, useful for client/server test

## Usage

1. From gstreamer container, go to the /src folder and create /build folder please!. Then run cmake and make:

```bash
cd /workspace/src
mkdir build
cd build
cmake .. && make
```

2. Go to /build/remote folder and execute remote app:

```bash
cd /workspace/src/build/remote
./gstreamer-remote
```

3. From yolo container, go to the python app folder and start the main.py directly. Modify the HOST and PORT specified in the code with the value of your containers info.

```bash
cd /workspace/src
python main.py
```

4. Run another gstreamer container instance

```bash
docker-compose run gst-container bin/bash
```

and,
    a - Copy the Legend.mp4 file into the folder where is locate the src code of the gstreamer-sandbox (/gstreamer-sandbox/src$)
    b - Execute the gstreamer pipeline local to connect to the remote: (replace )
```bash
gst-launch-1.0 filesrc location=Legend.mp4 ! decodebin ! x264enc ! rtph264pay ! udpsink host=172.X.X.X port=4000
```

5. Get the video/images or the specified output by yolo in the yolo container /workspace/src/ folder


## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
