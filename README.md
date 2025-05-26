# Using SVF as a Library

This repository demonstrates how to use SVF as a library in your project to analyze LLVM bitcode files. We provide examples for three different scenarios of using SVF.

## Prerequisites & Dependencies

SVF relies on the following libraries & tools:

- CMake (>=3.23)
- LLVM (<=16.0.6)
- Z3 (>=4.8.8)

## Scenario 1: Build from Scratch

In this scenario, we build SVF from source and use it directly from the build directory.

### Step 1: Build SVF

```shell
# Clone SVF
git clone https://github.com/SVF-tools/SVF.git
cd SVF

# Build SVF in Release mode
cmake -S ./ -B Release-build
cmake --build Release-build

# Or build SVF in Debug mode
cmake -S ./ -B Debug-build -DCMAKE_BUILD_TYPE=Debug
cmake --build Debug-build
```

### Step 2: Build SVF-example

```shell
# For Release build
cd SVF-example
cmake -B build -S ./ -DSVF_DIR=/path/to/SVF 
cmake --build build

# For Debug build
cd SVF-example
cmake -B build -S ./ -DSVF_DIR=/path/to/SVF -DCMAKE_BUILD_TYPE=Debug
cmake --build build
```

## Scenario 2: Install and Use

In this scenario, we install SVF to a specific directory and use it from there.

### Step 1: Build and Install SVF

```shell
# Clone SVF
git clone https://github.com/SVF-tools/SVF.git
cd SVF
```

If you build in Release mode, run
```
bash build.sh
cmake --install ./Release-build --prefix /path/to/install/dir
```

If you build in Debug mode, run
```
bash build.sh debug
cmake --install ./Debug-build --prefix /path/to/install/dir
```

### Step 2: Build SVF-example

```shell
cd SVF-example
cmake -B build -S ./ -DSVF_DIR=/path/to/install/dir
cmake --build build
```

## Scenario 3: NPM Installation

In this scenario, we use SVF installed through npm.

### Step 1: Install SVF via npm

```shell
npm install svf-lib
```

### Step 2: Build SVF-example

```shell
cd SVF-example
# Get npm root directory
NPM_ROOT=$(npm root)
# Set SVF_DIR to the SVF installation in npm
export SVF_DIR="$NPM_ROOT/SVF"
cmake -B build -S ./
cmake --build build
```

## Using the Example

After building in any of the above scenarios, you can run the example:

```shell
./build/svf-example ./data/example.ll
```

## Troubleshooting

### CMake Package Finding

If CMake cannot find SVF, ensure the installation directory is in your `CMAKE_PREFIX_PATH`:

```shell
# For Bash/Zsh
export CMAKE_PREFIX_PATH="$SVF_DIR${CMAKE_PREFIX_PATH:+:$CMAKE_PREFIX_PATH}"

# For Fish
set -px --path CMAKE_LIBRARY_PATH $SVF_DIR
```

### Library Path Issues

If you encounter library loading issues, ensure the library path is set correctly:

```shell
# For Bash/Zsh
export LD_LIBRARY_PATH="$SVF_DIR/lib:$LD_LIBRARY_PATH"

# For Fish
set -Upx LD_LIBRARY_PATH $SVF_DIR/lib
```

## Additional Information

For more detailed information about SVF setup and configuration, please refer to [the SVF wiki](https://github.com/svf-tools/SVF/wiki/Setup-Guide#getting-started).
