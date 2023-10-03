# esp32-rs Button Pad Controller (SparkFun)
Chaque touche appuyée renverra un retour visuel à l'utilisateur et mettra a jour une propriété du serveur BLE (la limite d'une touche à la fois a été conservée du button pad qui ne supporte pas plus).

### Setup (pour ubuntu)
1. Dépendances `apt install curl git build-essential python3 python3.8-venv python3-pip libclang-dev libudev-dev pkg-config`
2. Rustup & Rust (rust version manager: https://rustup.rs/) `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`
3. ldproxy pour générer le payload et espflash pour  flasher la carte `cargo install ldproxy espflash`
4. Pour lancer le projet, brancher la carte en USB et `cargo run`

### Technologies
- Esp32 Rust (avec l'esp32-c3 https://github.com/esp-rs/esp-rust-board qui supporte la STD de Rust)
    - Le support de la STD et donc du projet devrait marcher sur toutes les cartes qui supportent ESP-IDF (https://esp-rs.github.io/book/overview/using-the-standard-library.html) et qui possèdent une puce bluetooth avec le support du BLE
- Implémentation du SPI Sparkfun pour le Button Board Controller en suivant la documentation (https://www.sparkfun.com/datasheets/Widgets/ButtonPadControllerSPI_UserGuide_v2.pdf) **attention, certains nommages sont inversés dans certaines partie de la documentation MOSI <-> MISO**
    - Le SPI Sparkfun est non standard sur de nombreux points, Cf. les commentaires de la fiche produit : https://www.sparkfun.com/products/retired/9022
- BLE pour se commecter au traducteur de notes en utilisant la librairie NimBLE (https://lib.rs/crates/esp32-nimble)