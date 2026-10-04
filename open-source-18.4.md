# 따라ON 0.18.4 — 외부 라이브러리 소스 다운로드

> **2026-10-04 검토 정정:** 동봉 FFmpeg에서 Chromaprint를 통한 GPL FFTW 포함 근거가 확인됐습니다. `win64-lgpl`은 업스트림 파일명이며, 이를 근거로 순수 LGPL 구성이라고 판단하지 않습니다. 아래 소스 버전·해시 안내는 유효하지만, 현재 설치본의 배포 적합성 검토는 완료되지 않았습니다. [검토 근거](source-evidence/18.4/FFTW_FINDING.txt)

이 페이지는 따라ON 0.18.4-members1 설치본에 사용한 외부 라이브러리의 정확한 버전과 소스 위치를 안내합니다. 따라ON 자체의 비공개 코드는 포함하지 않습니다.

대상 설치파일 SHA-256: `ba8ddb211f4acea69ce392339aa7bae66d859abd6d3ed71ba62849681ec9e92f`

## Qt · PySide6 6.11.2

아래 파일은 공식 배포처에서 실제 다운로드하고 압축파일을 열어 확인했습니다. PySide6 소스에는 Shiboken 소스도 포함됩니다.

- [qtbase-everywhere-src-6.11.2.tar.xz](https://download.qt.io/official_releases/qt/6.11/6.11.2/submodules/qtbase-everywhere-src-6.11.2.tar.xz)
  - SHA-256: `5b2e00eccaf5a4d8c14134ffa0ea8dfd0a35ae1ffc7f8d87fa4305a1ed23cf22`
- [qtsvg-everywhere-src-6.11.2.tar.xz](https://download.qt.io/official_releases/qt/6.11/6.11.2/submodules/qtsvg-everywhere-src-6.11.2.tar.xz)
  - SHA-256: `d594337feca84c26fb67fe87b85e6a5c12fda404b611d905f9d138210c311876`
- [qtimageformats-everywhere-src-6.11.2.tar.xz](https://download.qt.io/official_releases/qt/6.11/6.11.2/submodules/qtimageformats-everywhere-src-6.11.2.tar.xz)
  - SHA-256: `cecd8900f34b6550076309bc94f62f828008b633a4239e0a08c86788f41001f8`
- [qtmultimedia-everywhere-src-6.11.2.tar.xz](https://download.qt.io/official_releases/qt/6.11/6.11.2/submodules/qtmultimedia-everywhere-src-6.11.2.tar.xz)
  - SHA-256: `967b5e02ec6b793cdb360622cd6e703132836af983208d678dae4b50f109cd9f`
- [pyside-setup-everywhere-src-6.11.2.tar.xz](https://download.qt.io/official_releases/QtForPython/pyside6/PySide6-6.11.2-src/pyside-setup-everywhere-src-6.11.2.tar.xz)
  - SHA-256: `cba47efbaad1bedd529725cbc14e21f156c7a19366f07b3edfbb076ffd7afdf8`

## FFmpeg 및 빌드 스크립트

설치본: `n8.1.3-14-g330caae0c1`, BtbN `win64-lgpl-8.1`.

FFmpeg 전체 커밋: `330caae0c1acccd2222edc52a05940c574561ce5`

BtbN 빌드 스크립트 커밋: `9acad4a9ef1583096af7836cc1e9c8cbcb4d3950`

설치된 ffmpeg.exe SHA-256: `f8ef72edbfe0e63d4ec01d50f39ef09e251998b157e82c20df1702a41e8ab91e`

- [ffmpeg-330caae0c1acccd2222edc52a05940c574561ce5.tar.gz](https://codeload.github.com/FFmpeg/FFmpeg/tar.gz/330caae0c1acccd2222edc52a05940c574561ce5)
  - SHA-256: `67b5876ee973a26f267280b2c1eb851a0ac7a502382d20e41b7a819111886af9`
- [btbn-build-9acad4a9ef1583096af7836cc1e9c8cbcb4d3950.zip](https://codeload.github.com/BtbN/FFmpeg-Builds/zip/9acad4a9ef1583096af7836cc1e9c8cbcb4d3950)
  - SHA-256: `6831eeef008b5955da5710900f74cac77b11a780058a283efc5d354a0e96e390`

두 압축파일을 실제 다운로드하고 압축 내부를 확인했습니다. BtbN 릴리스 태그의 빌드 스크립트와 위 고정 커밋의 281개 파일 내용도 일치했습니다.

- [빌드 설정 원문](source-evidence/18.4/FFMPEG_BUILD.txt)
- [하위 라이브러리별 저장소·고정 버전 목록](source-evidence/18.4/ffmpeg-dependency-sources.md)
- [소스 파일 다운로드 검증 기록](source-evidence/18.4/download-receipts.json)

### 빌드 버전 고정

원본 BtbN 스크립트의 `8.1` 옵션은 움직이는 `release/8.1` 브랜치를 가리킵니다. 현재 설치본과 같은 소스를 사용하려면 FFmpeg 소스를 가져온 직후, configure 전에 다음 커밋으로 고정해야 합니다.

```sh
git checkout --detach 330caae0c1acccd2222edc52a05940c574561ce5
```

빌드 대상과 옵션은 `win64 lgpl 8.1`이며, 실제 설정 원문은 위 링크에서 확인할 수 있습니다. 의존성 패치와 빌드 절차는 해당 BtbN 소스 압축파일에 포함됩니다. 이 안내가 비트 단위 재현 빌드 검증을 뜻하지는 않습니다.

## 확인 범위

Qt/PySide6, FFmpeg 본체와 빌드 스크립트의 위 7개 압축파일은 다운로드·해시·압축 구조를 확인했습니다. 하위 라이브러리는 빌드 스크립트에서 고정 버전을 추출했으며, 각 다운로드 주소의 확인 상태를 별도 목록에 표시합니다. 이 페이지는 소스 다운로드 안내이며, 전체 설치본의 고지·교체 가능성·기타 배포 조건 검토 완료를 뜻하지 않습니다.

확인일: 2026-10-04. 링크 문제가 있으면 kokow0507@naver.com으로 알려 주세요.
