## Tizen Studio Arch 가이드

이 가이드의 목적은 Tizen Studio CLI 버전을 설치하는 데 도움을 주는 것입니다. Arch Linux에서 Tizen Studio를 설치하는 가장 어려운 측면은 컴파일할 수 없는 'gnome-doc-util'과 같은 구식 의존성과 관련이 있습니다.

### 설치 방법
Arch Linux에서 Tizen Studio를 설치하려면 다음 단계를 따르세요:

1. 삼성 개발자 웹 사이트에서 Tizen Studio CLI의 최신 버전을 다운로드하십시오.
2. 아래 명령을 실행하여 패치에서 모든 필요한 종속성을 설치하십시오:

   ```
   yay -S procps-ng gettext dbus curl expect gtk2 grep zip make qemu-user libpng12 webkitgtk2-bin
   ```
   참고: 오래 걸리거나 문제가 발생하는 일부 종속성은 제외되었습니다.

   ```
   yay -S webkitgtk2-bin
   ```
   `webkitgtk2` 바이너리 버전을 설치하려면 `-bin`을 제거하여 직접 컴파일할 수 있습니다.
   
3. AUR 저장소에서 `debtap`을 설치하십시오.
4. [여기](https://packages.ubuntu.com/bionic/gnome-doc-utils)나 다른 소스에서 'gnome-doc-utils' 바이너리를 다운로드하십시오.
5. 필요한 모든 파일을 성공적으로 다운로드한 후에 `debtap gnome-doc-utils*deb`을 실행하십시오.
6. 명령은 `pacman`을 사용하여 설치할 수 있는 `.zst` 파일을 생성합니다.
7. 생성된 `.zst` 파일을 설치하려면 `pacman -U`를 사용하십시오. **이 방법은 권장되지 않으며 시스템이 손상될 수 있습니다.**
8. `yay` 또는 사용하는 다른 패키지 관리자를 사용하여 `gnome-desktop2` 를 설치하십시오. `build()`에서 `--disable-desktop-docs` 를 추가하여 'PKGBUILD'를 편집하십시오.

   ![](./readme/gnome_desktop2.png)

9. 위의 단계를 완료한 후에는 이 저장소에 패치를 적용하십시오:

   ```
   patch -u -b web-cli_Tizen_Studio_5.1_ubuntu-64.bin -i tizen_studio_cli.patch
   ```

10. 마지막으로, 실행 파일 './web-cli_Tizen_Studio_5.1_ubuntu-64.bin'을 실행하여 설치를 완료하십시오.

위 단계를 따르면 Arch Linux에 Tizen Studio를 성공적으로 설치할 수 있습니다.