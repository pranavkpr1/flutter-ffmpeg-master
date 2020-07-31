# flutter_ffmpeg 

![GitHub release](https://img.shields.io/badge/release-v0.2.10-blue.svg)
![](https://img.shields.io/pub/v/flutter_ffmpeg.svg)

FFmpeg plugin for Flutter. Supports iOS and Android.

<img src="https://github.com/tanersener/flutter-ffmpeg/raw/development/doc/assets/flutter-ffmpeg-logo-v2-cropped.png" width="240">

### 1. Features
- Based on `MobileFFmpeg`
- Includes both `FFmpeg` and `FFprobe`
- Supports
    - Both `Android` and `iOS`
    - Both Android (API Level 16+) and iOS (SDK 9.3+)
    - FFmpeg `v4.1`, `v4.2` and `v4.3-dev` releases
    - `arm-v7a`, `arm-v7a-neon`, `arm64-v8a`, `x86` and `x86_64` architectures on Android
    - `armv7`, `armv7s`, `arm64`, `arm64e`, `i386` and `x86_64` architectures on iOS
    - 24 external libraries

        `fontconfig`, `freetype`, `fribidi`, `gmp`, `gnutls`, `kvazaar`, `lame`, `libaom`, `libass`, `libiconv`, `libilbc`, `libtheora`, `libvorbis`, `libvpx`, `libwebp`, `libxml2`, `opencore-amr`, `opus`, `shine`, `snappy`, `soxr`, `speex`, `twolame`, `wavpack`

    - 4 external libraries with GPL license

        `vid.stab`, `x264`, `x265`, `xvidcore`

    - Concurrent execution
    - `zlib` and `MediaCodec` Android system libraries
    - `bzip2`, `zlib`, `iconv` iOS system libraries and `AudioToolbox`, `CoreImage`, `VideoToolbox`, `AVFoundation` iOS system frameworks

- Licensed under LGPL 3.0, can be customized to support GPL v3.0
- Includes eight different packages with different external libraries enabled in FFmpeg

<table>
<thead>
<tr>
<th align="center"></th>
<th align="center">min</th>
<th align="center">min-gpl</th>
<th align="center">https</th>
<th align="center">https-gpl</th>
<th align="center">audio</th>
<th align="center">video</th>
<th align="center">full</th>
<th align="center">full-gpl</th>
</tr>
</thead>
<tbody>
<tr>
<td align="center"><sup>external libraries</sup></td>
<td align="center">-</td>
<td align="center"><sup>vid.stab</sup><br><sup>x264</sup><br><sup>x265</sup><br><sup>xvidcore</sup></td>
<td align="center"><sup>gmp</sup><br><sup>gnutls</sup></td>
<td align="center"><sup>gmp</sup><br><sup>gnutls</sup><br><sup>vid.stab</sup><br><sup>x264</sup><br><sup>x265</sup><br><sup>xvidcore</sup></td>
<td align="center"><sup>lame</sup><br><sup>libilbc</sup><br><sup>libvorbis</sup><br><sup>opencore-amr</sup><br><sup>opus</sup><br><sup>shine</sup><br><sup>soxr</sup><br><sup>speex</sup><br><sup>twolame</sup><br><sup>wavpack</sup></td>
<td align="center"><sup>fontconfig</sup><br><sup>freetype</sup><br><sup>fribidi</sup><br><sup>kvazaar</sup><br><sup>libaom</sup><br><sup>libass</sup><br><sup>libiconv</sup><br><sup>libtheora</sup><br><sup>libvpx</sup><br><sup>libwebp</sup><br><sup>snappy</sup></td>
<td align="center"><sup>fontconfig</sup><br><sup>freetype</sup><br><sup>fribidi</sup><br><sup>gmp</sup><br><sup>gnutls</sup><br><sup>kvazaar</sup><br><sup>lame</sup><br><sup>libaom</sup><br><sup>libass</sup><br><sup>libiconv</sup><br><sup>libilbc</sup><br><sup>libtheora</sup><br><sup>libvorbis</sup><br><sup>libvpx</sup><br><sup>libwebp</sup><br><sup>libxml2</sup><br><sup>opencore-amr</sup><br><sup>opus</sup><br><sup>shine</sup><br><sup>snappy</sup><br><sup>soxr</sup><br><sup>speex</sup><br><sup>twolame</sup><br><sup>wavpack</sup></td>
<td align="center"><sup>fontconfig</sup><br><sup>freetype</sup><br><sup>fribidi</sup><br><sup>gmp</sup><br><sup>gnutls</sup><br><sup>kvazaar</sup><br><sup>lame</sup><br><sup>libaom</sup><br><sup>libass</sup><br><sup>libiconv</sup><br><sup>libilbc</sup><br><sup>libtheora</sup><br><sup>libvorbis</sup><br><sup>libvpx</sup><br><sup>libwebp</sup><br><sup>libxml2</sup><br><sup>opencore-amr</sup><br><sup>opus</sup><br><sup>shine</sup><br><sup>snappy</sup><br><sup>soxr</sup><br><sup>speex</sup><br><sup>twolame</sup><br><sup>vid.stab</sup><br><sup>wavpack</sup><br><sup>x264</sup><br><sup>x265</sup><br><sup>xvidcore</sup></td>
</tr>
<tr>
<td align="center"><sup>android system libraries</sup></td>
<td align="center" colspan=8><sup>zlib</sup><br><sup>MediaCodec</sup></td>
</tr>
<tr>
<td align="center"><sup>ios system libraries</sup></td>
<td align="center" colspan=8><sup>zlib</sup><br><sup>AudioToolbox</sup><br><sup>AVFoundation</sup><br><sup>CoreImage</sup><br><sup>iconv</sup><br><sup>VideoToolbox</sup><br><sup>bzip2</sup></td>
</tr>
</tbody>
</table>

### 2. Installation

Add `flutter_ffmpeg` as a dependency in your `pubspec.yaml file`.
  ```
dependencies:
    flutter_ffmpeg: ^0.2.10
  ```

#### 2.1 Packages

Installation of `FlutterFFmpeg` using `pub` enables the default package, which is based on `https` package. It is possible to enable other packages using the following steps.

##### 2.1.1 Android

- Edit `android/build.gradle` file and define package name in `ext.flutterFFmpegPackage` variable.

    ```
    ext {
        flutterFFmpegPackage  = "<package name>"
    }

    ```

##### 2.1.2 iOS

- Edit `ios/Podfile` file and modify the default `# Plugin Pods` block as follows. 
  Do not forget to specify package name in `<package name>` section.

    ```
    # Prepare symlinks folder. We use symlinks to avoid having Podfile.lock
    # referring to absolute paths on developers' machines.
    system('rm -rf .symlinks')
    system('mkdir -p .symlinks/plugins')
    plugin_pods = parse_KV_file('../.flutter-plugins')
    plugin_pods.each do |name, path|
      symlink = File.join('.symlinks', 'plugins', name)
      File.symlink(path, symlink)
      if name == 'flutter_ffmpeg'
          pod name+'/<package name>', :path => File.join(symlink, 'ios')
      else
          pod name, :path => File.join(symlink, 'ios')
      end
    end
    ```

##### 2.1.3 Package Names

The following table shows all package names defined for `flutter_ffmpeg`.
    
| Package | Main Release | LTS Release |
| :----: | :----: | :----: |
| min | min  | min-lts |
| min-gpl | min-gpl | min-gpl-lts |
| https | https | https-lts |
| https-gpl | https-gpl | https-gpl-lts |
| audio | audio | audio-lts |
| video | video | video-lts |
| full | full | full-lts |
| full-gpl | full-gpl | full-gpl-lts |


#### 2.2 Existing Applications

It is possible to add `flutter_ffmpeg` to existing applications using [Add-to-App](https://github.com/flutter/flutter/wiki/Add-Flutter-to-existing-apps) guide.

Please execute the following additional steps if you are integrating into an iOS application.

1. Go to `Build Phases` of `Pods` -> `FlutterPluginRegistrant` target and add all frameworks under the `Pods/mobile-ffmpeg-<package name>` directory to the `Link Binary With Libraries` section

2. Go to `Build Phases` of `Pods` -> `FlutterPluginRegistrant` target and add all system libraries/frameworks listed in Step 4 of [Importing-Frameworks](https://github.com/tanersener/mobile-ffmpeg/wiki/Importing-Frameworks) guide to the `Link Binary With Libraries` section

3. Go to `Build Phases` of `Pods` -> `FlutterPluginRegistrant` target and add `AVFoundation` system framework to the `Link Binary With Libraries` section

#### 2.3 LTS Releases

`flutter_ffmpeg` is published in two different variants: `Main Release` and `LTS Release`. Both releases share the same source code but is built with different settings. Below you can see the changes between the two.

In order to install the `LTS` variant, install the `https-lts` package using instructions in `2.1` or append `-lts` to the package name you are using. 

<table>
<thead>
    <tr>
        <th align="center"></th>
        <th align="center">Main Release</th>
        <th align="center">LTS Release</th>
    </tr>
</thead>
<tbody>
    <tr>
        <td align="center">Android API Level</td>
        <td align="center">24</td>
        <td align="center">16</td>
    </tr>
    <tr>
        <td align="center">Android Camera Access</td>
        <td align="center">Yes</td>
        <td align="center">-</td>
    </tr>
    <tr>
        <td align="center">Android Architectures</td>
        <td align="center">arm-v7a-neon<br>arm64-v8a<br>x86<br>x86-64</td>
        <td align="center">arm-v7a<br>arm-v7a-neon<br>arm64-v8a<br>x86<br>x86-64</td>
    </tr>
    <tr>
        <td align="center">Xcode Support</td>
        <td align="center">10.1</td>
        <td align="center">7.3.1</td>
    </tr>
    <tr>
        <td align="center">iOS SDK</td>
        <td align="center">12.1</td>
        <td align="center">9.3</td>
    </tr>
    <tr>
        <td align="center">iOS Architectures</td>
        <td align="center">arm64<br>arm64e<br>x86-64</td>
        <td align="center">armv7<br>arm64<br>i386<br>x86-64</td>
    </tr>
</tbody>
</table>

### 3. Using

1. Execute FFmpeg commands.

    - Use execute() method with a single command line  
    ```
    import 'package:flutter_ffmpeg/flutter_ffmpeg.dart';

    final FlutterFFmpeg _flutterFFmpeg = new FlutterFFmpeg();

    _flutterFFmpeg.execute("-i file1.mp4 -c:v mpeg4 file2.mp4").then((rc) => print("FFmpeg process exited with rc $rc"));
    ```
    
    - Use executeWithArguments() method with an array of arguments  

    ```
    import 'package:flutter_ffmpeg/flutter_ffmpeg.dart';

    final FlutterFFmpeg _flutterFFmpeg = new FlutterFFmpeg();

    var arguments = ["-i", "file1.mp4", "-c:v", "mpeg4", "file2.mp4"];
    _flutterFFmpeg.executeWithArguments(arguments).then((rc) => print("FFmpeg process exited with rc $rc"));
    ```

2. Execute FFprobe commands.

    - Use execute() method with a single command line  
    ```
    import 'package:flutter_ffmpeg/flutter_ffmpeg.dart';

    final FlutterFFprobe _flutterFFprobe = new FlutterFFprobe();

    _flutterFFprobe.execute("-i file1.mp4").then((rc) => print("FFprobe process exited with rc $rc"));
    ```
    
    - Use executeWithArguments() method with an array of arguments  

    ```
    import 'package:flutter_ffmpeg/flutter_ffmpeg.dart';

    final FlutterFFprobe _flutterFFprobe = new FlutterFFprobe();

    var arguments = ["-i", "file1.mp4"];
    _flutterFFprobe.executeWithArguments(arguments).then((rc) => print("FFprobe process exited with rc $rc"));
    ```

3. Check execution output. Zero represents successful execution, non-zero values represent failure.
    ```
   
   final FlutterFFmpegConfig _flutterFFmpegConfig = new FlutterFFmpegConfig();
   
    _flutterFFmpegConfig.getLastReturnCode().then((rc) => print("Last rc: $rc"));

    _flutterFFmpegConfig.getLastCommandOutput().then((output) => print("Last command output: $output"));
    ```

4. Stop an ongoing operation. Note that this function does not wait for termination to complete and returns immediately.
    ```
    _flutterFFmpeg.cancel();
    ```

5. Get media information for a file.
    - Print all fields
    ```
   final FlutterFFprobe _flutterFFprobe = new FlutterFFprobe();

    _flutterFFprobe.getMediaInformation("<file path or uri>").then((info) => print(info));
    ```
    - Print selected fields
    ```
   final FlutterFFprobe _flutterFFprobe = new FlutterFFprobe();

    _flutterFFprobe.getMediaInformation("<file path or uri>").then((info) {
        print("Media Information");

        print("Path: ${info['path']}");
        print("Format: ${info['format']}");
        print("Duration: ${info['duration']}");
        print("Start time: ${info['startTime']}");
        print("Bitrate: ${info['bitrate']}");

        if (info['streams'] != null) {
            final streamsInfoArray = info['streams'];

            if (streamsInfoArray.length > 0) {
                for (var streamsInfo in streamsInfoArray) {
                    print("Stream id: ${streamsInfo['index']}");
                    print("Stream type: ${streamsInfo['type']}");
                    print("Stream codec: ${streamsInfo['codec']}");
                    print("Stream full codec: ${streamsInfo['fullCodec']}");
                    print("Stream format: ${streamsInfo['format']}");
                    print("Stream full format: ${streamsInfo['fullFormat']}");
                    print("Stream width: ${streamsInfo['width']}");
                    print("Stream height: ${streamsInfo['height']}");
                    print("Stream bitrate: ${streamsInfo['bitrate']}");
                    print("Stream sample rate: ${streamsInfo['sampleRate']}");
                    print("Stream sample format: ${streamsInfo['sampleFormat']}");
                    print("Stream channel layout: ${streamsInfo['channelLayout']}");
                    print("Stream sar: ${streamsInfo['sampleAspectRatio']}");
                    print("Stream dar: ${streamsInfo['displayAspectRatio']}");
                    print("Stream average frame rate: ${streamsInfo['averageFrameRate']}");
                    print("Stream real frame rate: ${streamsInfo['realFrameRate']}");
                    print("Stream time base: ${streamsInfo['timeBase']}");
                    print("Stream codec time base: ${streamsInfo['codecTimeBase']}");

                    final metadataMap = streamsInfo['metadata'];
                    if (metadataMap != null) {
                        print('Stream metadata encoder: ${metadataMap['encoder']}');
                        print('Stream metadata rotate: ${metadataMap['rotate']}');
                        print('Stream metadata creation time: ${metadataMap['creation_time']}');
                        print('Stream metadata handler name: ${metadataMap['handler_name']}');
                    }
    
                    final sideDataMap = streamsInfo['sidedata'];
                    if (sideDataMap != null) {
                        print('Stream side data displaymatrix: ${sideDataMap['displaymatrix']}');
                    }
                }
            }
        }

    ```

6. Enable log callback and redirect all `FFmpeg`/`FFprobe` logs to a console/file/widget.
    ```
    void logCallback(int level, String message) {
        print(message);
    }
    ...
    _flutterFFmpegConfig.enableLogCallback(this.logCallback);
    ```

7. Enable statistics callback and follow the progress of an ongoing `FFmpeg` operation.
    ```
    void statisticsCallback(int time, int size, double bitrate, double speed, int videoFrameNumber, double videoQuality, double videoFps) {
        print("Statistics: time: $time, size: $size, bitrate: $bitrate, speed: $speed, videoFrameNumber: $videoFrameNumber, videoQuality: $videoQuality, videoFps: $videoFps");
    }
    ...
    _flutterFFmpegConfig.enableStatisticsCallback(this.statisticsCallback);
    ```

8. Poll statistics without implementing statistics callback.
    ```
    _flutterFFmpegConfig.getLastReceivedStatistics().then((stats) => print(stats));
    ```

9. Reset statistics before starting a new operation.
    ```
    _flutterFFmpegConfig.resetStatistics();
    ```

10. Set log level.
    ```
    _flutterFFmpegConfig.setLogLevel(LogLevel.AV_LOG_WARNING);
    ```

11. Register your own fonts by specifying a custom fonts directory, so they are available to use in `FFmpeg` filters. Please note that this function can not work on relative paths, you need to provide full file system path.
    ```
    _flutterFFmpegConfig.setFontDirectory("<folder with fonts>");
    ```

12. Use your own `fontconfig` configuration.
    ```
    _flutterFFmpegConfig.setFontconfigConfigurationPath("<fontconfig configuration directory>");
    ```

13. Disable log functionality of the library. Logs will not be printed to console and log callback will be disabled.
    ```
    _flutterFFmpegConfig.disableLogs();
    ```

14. Disable statistics functionality of the library. Statistics callback will be disabled but the last received statistics data will be still available.
    ```
    _flutterFFmpegConfig.disableStatistics();
    ```

15. List enabled external libraries.
    ```
    _flutterFFmpegConfig.getExternalLibraries().then((packageList) {
         packageList.forEach((value) => print("External library: $value"));
    });
    ```
16. Create new `FFmpeg` pipe. 
    ```
    _flutterFFmpegConfig.registerNewFFmpegPipe().then((path) {
         then((stats) => print("New ffmpeg pipe at $path"));
    });
    ```

### 4. Tips

- `flutter_ffmpeg` uses file system paths, it does not know what an `assets` folder or a `project` folder is. So you can't use resources on those folders directly, you need to provide full paths of those resources.

- `flutter_ffmpeg` requires ios deployment target to be at least `9.3`. 
  If you don't specify a deployment target or set a value smaller than `9.3` then your build will fail with the following error.
   
   ```
    Resolving dependencies of `Podfile`
    [!] CocoaPods could not find compatible versions for pod "flutter_ffmpeg":
      In Podfile:
        flutter_ffmpeg (from `.symlinks/plugins/flutter_ffmpeg/ios`)
    
    Specs satisfying the `flutter_ffmpeg (from `.symlinks/plugins/flutter_ffmpeg/ios`)` dependency were found, but they required a higher minimum
    deployment target.
    ```
    
  You can fix this issue by adding `platform :ios, '9.3'` definition to your `ios/Podfile` file.

    ```
    platform :ios, '9.3'
    ```
    
- `flutter_ffmpeg` includes native libraries that require ios deployment target to be at least `9.3`. 
  If a deployment target is not set or a value smaller than `9.3` is used then your build will fail with the following error.
   
    ```
    ld: targeted OS version does not support use of thread local variables in __gnutls_rnd_deinit for architecture x86_64
    clang: error: linker command failed with exit code 1 (use -v to see invocation)
    ```

  Unfortunately the latest versions of `Flutter` and `Cocoapods` have some issues about setting ios deployment target from `Podfile`.
  Having `platform :ios, '9.3'` in your `Podfile` is not enough. `Runner` project still uses the default value `8.0`.
  You need to open `Runner.xcworkspace` in `Xcode` and set `iOS Deployment Target` of `Runner` project to `9.3` manually.
    
    <img src="https://github.com/tanersener/flutter-ffmpeg/raw/development/doc/assets/tip_runner_deployment_target.png" width="480">

- Enabling `ProGuard` on releases older than `v0.2.4` causes linking errors. Please add the following rule inside your `proguard-rules.pro` file to preserve necessary method names and prevent linking errors.

    ```
    -keep class com.arthenica.mobileffmpeg.Config {
        native <methods>;
        void log(int, byte[]);
        void statistics(int, float, float, long , int, double, double);
    }
    ```

- `ffmpeg` requires a valid `fontconfig` configuration to render subtitles. Unfortunately, Android does not include a default `fontconfig` configuration. 
So if you do not register a font or specify a `fontconfig` configuration under Android, then the burning process will not produce any errors but subtitles won't be burned in your file. 
You can overcome this situation by registering a font using `setFontDirectory` method or specifying your own `fontconfig` configuration using `setFontconfigConfigurationPath` method.

- By default, Xcode compresses `PNG` files during packaging. If you use `.png` files in your commands make sure you set the following two settings to `NO`. If one of them is set to `YES`, your operations may fail with `Error while decoding stream #0:0: Generic error in an external library` error.

    <img src="https://github.com/tanersener/flutter-ffmpeg/raw/development/doc/assets/tip_png_files.png" width="720">

- Some `flutter_ffmpeg` packages include `libc++_shared.so` native library. If a second library which also includes `libc++_shared.so` is added as a dependency, `gradle` fails with `More than one file was found with OS independent path 'lib/x86/libc++_shared.so'` error message.

  You can fix this error by adding the following block into your `build.gradle`.
  ```
  android {
      packagingOptions {
          pickFirst 'lib/x86/libc++_shared.so'
          pickFirst 'lib/x86_64/libc++_shared.so'
          pickFirst 'lib/armeabi-v7a/libc++_shared.so'
          pickFirst 'lib/arm64-v8a/libc++_shared.so'
      }
  }
  ```

### 5. Updates

Refer to [Changelog](CHANGELOG.md) for updates.

### 6. License

This project is licensed under the LGPL v3.0. However, if installation is customized to use a package with `-gpl` postfix (min-gpl, https-gpl, full-gpl) then `FlutterFFmpeg` is subject to the GPL v3.0 license.

Digital assets used in test applications are published in the public domain.

### 7. Contributing

Feel free to submit issues or pull requests.

### 8. See Also

- [FFmpeg](https://www.ffmpeg.org)
- [Mobile FFmpeg Wiki](https://github.com/tanersener/mobile-ffmpeg/wiki)
- [FFmpeg License and Legal Considerations](https://ffmpeg.org/legal.html)
