# Sonu Birthday → Birthday Surprise → Appreciation

This repository packages three connected stages:

1. `site-root/` — the Sonu birthday landing page. Its final button leads to `birthday/index.html`.
2. `birthday/` — the second birthday experience. Its Continue button stays locked until **18 November 2026, 00:00 IST**.
3. `private/appreciation-site.tar.gz.enc` — the appreciation site, encrypted and excluded from deployment before the deadline. After release, it is published at `/appreciation/`.

## GitHub Pages setup

- Set Pages source to **GitHub Actions**.
- Keep workflow permissions sufficient to deploy Pages.
- Add/update the repository Actions secret named `SORRY_DECRYPTION_KEY` with the value from the separately supplied key file. Do not commit or upload the key file.
- Push the files to `main`. Before the deadline, deployments include only the first two stages. The scheduled workflow runs at 18:30 UTC on 17 November 2026 (00:00 IST on 18 November); scheduled GitHub Actions may start a little late, so the lock itself also checks the exact deadline.

The appreciation archive uses OpenSSL AES-256-CBC with PBKDF2 (200,000 iterations). Keep the secret key private.


## Final GitHub Pages setup

- Upload the contents of this folder to the root of your new GitHub repository and use the `main` branch.
- Enable GitHub Pages with **GitHub Actions** as the build and deployment source.
- Add the repository Actions secret named `SORRY_DECRYPTION_KEY` using the separate private key file supplied with this package. Do not commit that key file or paste the key into any public file.
- The workflow publishes the birthday site and its audio immediately. The encrypted appreciation archive remains gated until **18 November 2026 at 00:00 IST**.
- The hidden song is expected at `site-root/audio/sonu-surprise.mp3`; the workflow copies it into the published `out/audio/` directory.


## Make a Wish game — automatic browser build

The encrypted appreciation archive now includes the original `make_a_wish.py` source and a Pygbag-compatible entry point at `game_src/main.py`. After the scheduled unlock, the workflow decrypts the archive, installs Python 3.11 plus Pygbag/pygame-ce/NumPy, builds the game, and copies the generated browser files into `out/appreciation/game/` before uploading the GitHub Pages artifact. The game is launched by the **Let's Celebrate** button in `birthday-wishes.html`.

No plaintext appreciation folder or generated game build is committed to the repository. The appreciation archive remains encrypted until the release deadline. Keep the Actions secret `SORRY_DECRYPTION_KEY` set to the value in the separately supplied key instructions; do not upload that key file to GitHub.

The workflow will fail rather than publish a broken game if the Pygbag build does not produce `game/index.html`.
