# CAS Gradle Overlay

Repositori ini berisikan file untuk pebangunan CAS menggunakan gradle

## Versi

- CAS `5.3.x`

## Kebutuhan

- JDK 1.8+

## Configuration

Direktori bernama `etc` mengandung file konfigurasi dan direktori yang harus di-copy-kan adalah `/etc/cas/config`..

## Adding Modules

Modul CAS dispesifikasikan oleh `dependencies` dalam file [Gradle build script](build.gradle):

```gradle
dependencies {
    compile "org.apereo.cas:cas-server-webapp-tomcat:${project.'cas.version'}@war"
    compile "org.apereo.cas:cas-server-some-module:${project.'cas.version'}"
    ...
}
```

Referensi:

- https://docs.gradle.org/current/userguide/artifact_dependencies_tutorial.html
- https://docs.gradle.org/current/userguide/dependency_management.html

## Build

Untuk mengetahui apa saja yang dapat dilakukan dengan command Gradle, tuliskan perintah:

```bash
./build.sh help
```

Untuk membuat package aplikasi final, jalankan perintah:

```bash
./build.sh package
```

Untuk memperbaharui versi `SNAPSHOT` run:

```bash
./build.sh package --refresh-dependencies
```

### Bersihkan Cache Gradle

Caranya dalah dengan:

```bash
# Only do this when absolutely necessary!
rm -rf $HOME/.gradle/caches/
```

### Build Tasks

CAaranya gunakan perintah:

```bash
 ./gradlew[.bat] tasks
```

## Deployment

- Buat file keystore dengan nama `thekeystore` di dalam `/etc/cas` di Linux. Atau `c:/etc/cas` di Windows.
- Gunakan password `changeit` untuk keystorenya dan sertifikat.
- Pastikan keystore sudah di-load dengan key dan sertifikat server, dengan mengeceknya di `./etc/cas/config/cas.properties`:

```properties
server.ssl.keyStore=file:/etc/cas/thekeystore
server.ssl.keyStorePassword=changeit
server.ssl.keyPassword=changeit
```

Jika deployment berhasil, silakan cek pada browser dengan URL:

- `http://cas.server.name:8080/cas`
- `https://cas.server.name:8443/cas`

Port dapat disesuaikan dengan pengaturan port yang sudah dilakukan sebelumnya

## Dengan Eksekusi WAR

Jalankan CAS Web dengan perintah:

```bash
./build.sh run
```

## Spring Boot

Menggunakan Spring Boot

```bash
./build.sh bootrun
```

## Command Line Shell

```bash
./build.sh cli
```
