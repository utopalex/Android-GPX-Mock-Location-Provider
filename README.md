# AndroidMockGpx

This open source Android application allows you to stream GPX files through the Mock Location provider to simulate GPS on the device.

## Installing and granting permissions

1. Build and install APK (requires to use a Debug build)
2. Enable "mock locations" on Android device.
        Settings > Developer Options > Allow Mock Locations
        grant to "AndroidMockGpx" or grant via adb: `adb shell appops set com.twolinessoftware.android android:mock_location allow
3. Install "OI File Manager" on android device.
        http://www.openintents.org/filemanager/ (optional)

4. Run AndroidMockGpx, when prompted: Grant Location and File Access Permission

## Running with UI

Select a file (either use the file chooser icon if you have OI Filemanager installed) or type file path location directly.

Below, enter either "0" if you have working timestamps in your GPX trace and want to replay them in the right time, or any other value in milliseconds if you want to replay them faster.

Press *Start*.

## Running without UI

Once all permissions to the app have been granted you can also run it headless.

This can be used for automated tests.

### Replay a GPX file

```shell
adb shell am start-foreground-service -n com.twolinessoftware.android/.PlaybackService -e filename "/storage/emulated/10/file2.gpx" -e delayTimeOnReplay 0
```

### Jump to a certain static location

San Francisco:

```shell
adb shell am start-foreground-service -n com.twolinessoftware.android/.PlaybackService -e location "'San Francisco'"
```

Berlin:

```shell
adb shell am start-foreground-service -n com.twolinessoftware.android/.PlaybackService -e location "Berlin"
```

## Troubleshooting

If the file has been properly parsed you should see message like these via logcat: `PlaybackService: Sending Point in:6962ms`.

Once it replays positions, you should see messages like ```D/SendLocation: Sending update for gps```

Ensure you have setup mock position. The application needs to be also granted location and read file access permission (READ_STORAGE).

## Report Issues/Bugs

File a bug here on github, or feel free to submit merge-requests.

There a lot of different GPX file formats out there, this application can perform best on those generated by gpsbabel.
