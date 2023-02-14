# User manual

Replace ```<YOUR_PATH>``` with the path of your choice e.g. ```~/Documents```.

## Dependencies

### Libraries
```bash
sudo apt install libipe-dev libpng-dev libjpeg-dev libspiro-dev
```

### ipe_generator
```bash
cd <YOUR_PATH>
git clone https://github.com/Teusner/ipe_generator.git
cd ipe_generator
mkdir build
cd build
cmake ..
make -j8
sudo make install
```

### fmt
```bash
cd <YOUR_PATH>
git clone https://github.com/fmtlib/fmt.git
cd fmt
mkdir build
cd build
cmake ..
make -j8
sudo make install
```

### rapidyaml
```bash
cd <YOUR_PATH>
git clone https://github.com/biojppm/rapidyaml.git
cd rapidyaml
mkdir build
cd build
cmake ..
make -j8
sudo make install
```

## Install

```bash
cd <YOUR_PATH>
git clone https://github.com/Teusner/Wakeboat.git
cd Sillage
mkdir build
cd build
cmake ..
make -j8
```

## Setup

```bash
cd <YOUR_PATH>/Wakeboat
git submodule init
git submodule update
```

## Generate .ipe files
```bash
cd <YOUR_PATH>/Wakeboat
mkdir output
cd build
cmake ..
make -j8
./main --path=../output
```

## Generate .png images
```bash
cd <YOUR_PATH>/Wakeboat
cd scripts
./ipe_convert.bash ../output
```

## Generate .mp4 video
```bash
cd <YOUR_PATH>/Wakeboat
cd scripts
./ipe_convert.bash ../output
./video.bash ../output
```

You will get ```<YOUR_PATH/Wakeboat/scripts/Wake.mp4```.

You can watch it with ```vlc``` for example ```vlc <YOUR_PATH/Wakeboat/scripts/Wake.mp4```.
