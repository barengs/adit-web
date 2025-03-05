# ADIT (Aplikasi Akademik Terintegrasi) Front End - UMI

Merupakan sistem tata kelola universitas terintegrasi.
Terdiri atas beberapa aplikasi yang saling terhubung dengan teknologi terkini.

## APLIKASI

- PMB (sistem penerimaan mahasiswa baru)
- AKADEMIK (sistem tata kelola akademik seperti matakuliah, dosen, KRS, KHS, penilaian dan lainnya.)
- KEUANGAN (sistem tata kelola keuangan kampus)
- LMS (sistem pengajaran daring)
- MODIS (sistem infromasi kampus berbasis mobile)

# sv

Everything you need to build a Svelte project, powered by [`sv`](https://github.com/sveltejs/cli).

## Copy a project

If you're seeing this, you've probably already done this step. Congrats!

```bash
# clone a project in the current directory
git clone https://github.com/barengs/adit-web.git
```

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
# run project
cd adit-web
npm install
git branch new_your_branch
git checkout new_your_branch
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

## Building

To create a production version of your app:

```bash
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://svelte.dev/docs/kit/adapters) for your target environment.
