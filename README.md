# Flutter Android SDK Docker Image

[![Docker Pulls](https://img.shields.io/docker/pulls/julesreyn/flutter-android-sdk.svg)](https://hub.docker.com/r/julesreyn/flutter-android-sdk)

This Docker image provides a complete setup with Flutter and Android SDK, tailored for building Flutter applications, including APKs for Android.

## Image Features

- **Flutter SDK**: Pre-installed Flutter SDK for building mobile apps.
- **Android SDK**: Includes Android SDK, platform-tools, and build-tools (Android 33 and build-tools 34.0.0).
- **Android Licenses**: Pre-accepted Android SDK licenses for non-interactive use.
- **Utilities**: Comes with essential tools such as `curl`, `git`, and `unzip`.

## Quick Start

You can use this Docker image to build Flutter APKs by pulling the image and running the following commands.

### Example `Dockerfile`

Here’s an example of how you can use this base image to build your Flutter APK:

```Dockerfile
FROM julesreyn/flutter-android-sdk:jdk24-android33-flutter3.24.3

USER root

WORKDIR /home/builder/app

COPY . .

RUN chown -R builder:builder /home/builder/app

USER builder

RUN flutter pub get
RUN flutter build apk --release

CMD ["tail", "-f", "/dev/null"]
```

### Build your APK

1. Clone your Flutter project into a directory.
2. Create a Dockerfile similar to the example above.
3. Build the Docker image:

```bash
docker build -t my-flutter-app .
```

4. Run the container to build your APK:

```bash
docker run --rm -v "$PWD":/home/builder/app my-flutter-app
```

Your APK will be available in the `build/app/outputs/flutter-apk/` directory of your project.

## Environment Variables

- `ANDROID_SDK_ROOT`: Points to the Android SDK installation.
- `FLUTTER_HOME`: Path to the Flutter SDK installation.
- `PATH`: Ensures the Flutter and Android tools are available in the environment.

## Cleaning up Cached Files

To keep the image as lightweight as possible, several unused Flutter engine artifacts have been removed, including:

- Arm architectures (`android-arm`, `android-arm64`, etc.)
- Other platforms' engine artifacts (`darwin-x64`, `windows-x64`, etc.)

## Docker Images

The following table shows available image versions. The `latest` tag points to the minimal base image.

| Docker Tag | JDK Version | Flutter Version | Android SDK | Artifacts Included | Image Size |
|------------|-------------|-----------------|-------------|-------------------|------------|
| jdk24-android33-flutter3.24.3 (latest) | OpenJDK 24 | 3.24.3 | 34.0.0 | None | 2.56GB |
| jdk24-android33-flutter3.24.3-full | OpenJDK 24 | 3.24.3 | 34.0.0 | All platforms | 2.56GB |
| jdk24-android33-flutter3.24.3-android-arm | OpenJDK 24 | 3.24.3 | 34.0.0 | android-arm | 2.56GB |
| jdk24-android33-flutter3.24.3-android-arm64 | OpenJDK 24 | 3.24.3 | 34.0.0 | android-arm64 | 2.56GB |
| jdk24-android33-flutter3.24.3-android-x64 | OpenJDK 24 | 3.24.3 | 34.0.0 | android-x64 | 2.56GB |
| jdk24-android33-flutter3.24.3-linux-x64 | OpenJDK 24 | 3.24.3 | 34.0.0 | linux-x64 | 2.56GB |
| jdk24-android33-flutter3.24.3-darwin-x64 | OpenJDK 24 | 3.24.3 | 34.0.0 | darwin-x64 | 2.56GB |
| jdk24-android33-flutter3.24.3-windows-x64 | OpenJDK 24 | 3.24.3 | 34.0.0 | windows-x64 | 2.56GB |
| jdk17-android33-flutter3.24.3 | OpenJDK 17 | 3.24.3 | 34.0.0 | None | 2.58GB |
| jdk17-android33-flutter3.24.3-full | OpenJDK 17 | 3.24.3 | 34.0.0 | All platforms | 2.58GB |
| jdk17-android33-flutter3.24.3-android-arm | OpenJDK 17 | 3.24.3 | 34.0.0 | android-arm | 2.58GB |
| jdk17-android33-flutter3.24.3-android-arm64 | OpenJDK 17 | 3.24.3 | 34.0.0 | android-arm64 | 2.58GB |
| jdk17-android33-flutter3.24.3-android-x64 | OpenJDK 17 | 3.24.3 | 34.0.0 | android-x64 | 2.58GB |
| jdk17-android33-flutter3.24.3-linux-x64 | OpenJDK 17 | 3.24.3 | 34.0.0 | linux-x64 | 2.58GB |
| jdk17-android33-flutter3.24.3-darwin-x64 | OpenJDK 17 | 3.24.3 | 34.0.0 | darwin-x64 | 2.58GB |
| jdk17-android33-flutter3.24.3-windows-x64 | OpenJDK 17 | 3.24.3 | 34.0.0 | windows-x64 | 2.58GB |

All images share the same base configuration but differ in included platform-specific artifacts:
- Base image (latest): Minimal setup with no platform artifacts
- Full (-full): Includes artifacts for all platforms
- Platform-specific (-android-arm, -android-arm64, etc.): Include only specific platform artifacts

Images are automatically built and pushed to Docker Hub via GitHub Actions when changes are made to the main branch.

## License

This Docker image is maintained by **Jules Reynaud**. For any issues or contributions, feel free to reach out here : docker-hub-android-s.handled958@passmail.net.