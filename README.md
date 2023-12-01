# Publication

[1] "An Empirical Study of Functional Bugs in Android Apps" by Yiheng Xiong, Mengqian Xu, Ting Su, Jingling Sun, Jue Wang, He Wen, Geguang Pu, Jifeng He and Zhendong Su. In Proceedings of the 32nd ACM SIGSOFT International Symposium on Software Testing and Analysis (ISSTA 2023).
```
@inproceedings{functionalbugs2023,
  title={An Empirical Study of Functional Bugs in Android Apps},
  author={Xiong, Yiheng and Xu, Mengqian and Su, Ting and Sun, Jingling and Wang, Jue and Wen, He and Pu, Geguang and He, Jifeng and Su, Zhendong},
  booktitle={Proceedings of the 32nd ACM SIGSOFT International Symposium on Software Testing and Analysis},
  pages={1319--1331},
  year={2023},
  doi = {10.1145/3597926.3598138},
  series = {ISSTA 2023}
}
```

*You can find more about our work on testing/analyzing Android apps at this [website](https://tingsu.github.io/files/mobile-app-analysis.html)*.

# Replication Package
This repository contains all the artifacts (including the dataset and the tool Regdroid) in our study.

## Directory Structure

    home
        |
        | --- Dataset:                      The bug list of 399 bug reports
        | --- RegDroid:                     The source code of RegDroid
             |
             | --- start.py:                The entry of RegDroid, which accepts the parameters
             | --- regdroid.py              The main module of RegDroid
             | --- executor.py              The execution module of RegDroid

## RegDroid

### Getting Started


#### Requirements

- Android SDK: API26+
- python 3.8
- We use some libraries (e.g., uiautomator2, androguard, cv2) provided by python, you can add them as prompted, for example:

```
pips install uiautomator2
```

#### Setting up

You can create an emulator before running RegDroid. See [this link](https://stackoverflow.com/questions/43275238/how-to-set-system-images-path-when-creating-an-android-avd) for how to create avd using [avdmanager](https://developer.android.com/studio/command-line/avdmanager).
The following sample command will help you create an emulator, which will help you to start using RegDroid quickly：

```
sdkmanager "system-images;android-26;google_apis;x86"
avdmanager create avd --force --name Android8.0 --package 'system-images;android-26;google_apis;x86' --abi google_apis/x86 --sdcard 512M --device "pixel_xl"
```

Next, you can start two identical emulators and assign their port numbers with the following commands:

```
emulator -avd Android8.0 -read-only -port 5554
emulator -avd Android8.0 -read-only -port 5556
```

#### Run

If you have downloaded our project and configured the environment, you only need to enter ``download_path/tool/RegDroid`` to execute our sample app with the following command:

```
python3 start.py -app_path ./App/AmazeFileManager-3.7.1.apk -emulator_path  path_to_emulator -app_path ./App/AmazeFileManager-3.7.2.apk  -append_device emulator-5554 -append_device emulator-5556 -output  3.7.1-3.7.2  -testcase_count 1 -event_num 20
```

Here,

``-app_path``: the file path of APK

``-emulator_path ``: the path to the emulator

``-append_device``: the serial number of devices used in the test, which can be obtained by executing "adb devices" in the terminal.

``-output``: the output directory under /Tool/Output/app_package_name/

``-testcase_count`` The number of rounds that you want to test.

``-event_num`` The number of events in per round of test.

