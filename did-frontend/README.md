# This is a Verifiable Credential (VC) Gated Website

- My hosted example website: https://stephs-vc-gated-dapp.vercel.app
- In order to see the gated part of the website, you need a [KYCAgeCredential Verifiable Credential](https://www.notion.so/oceans404/How-to-get-a-KYCAgeCredential-Verifiable-Credential-f3d34e7c98ec4147b6b2fae79066c4f6?pvs=4) with a birthday after January 1, 2023, held in the Polygon ID Mobile wallet app.

<img width="1292" alt="Screenshot 2023-06-06 at 10 30 51 AM" src="https://github.com/oceans404/vc-gated-website/assets/91382964/53fe84f1-18ae-4050-9517-5e54ec1de982">

## About

This is an opinionated template for creating VC gated dapps with

- frontend library: [NextJS](https://nextjs.org/)
- component library: [Chakra](https://chakra-ui.com/)
- wallet connection libraries: [Rainbowkit](https://www.rainbowkit.com/) using WalletConnect v2, wagmi, & viem hooks

## How to run locally

#### 0. Follow server setup instructions

Before starting the frontend, run the server by following [the server instructions](https://github.com/oceans404/fullstack-polygon-id-vc-gated-dapp/tree/main/server). You need the ngrok url from the server in order to start the frontend.

#### 1. Install frontend dependencies with --legacy-peer-deps

Make sure to run the install command with the --legacy-peer-deps flag.

```bash
yarn install
```

#### 2. Create a .env file by copying my sample

```bash
cp .env.sample .env;
```

Update your .env with the NEXT_PUBLIC_VERIFICATION_SERVER_PUBLIC_URL variable to your hosted server ngrok url. If you're hosting in production with render, use the render url for this variable.

Visit https://cloud.walletconnect.com/ and create a new project (free and takes 2m). Update NEXT_PUBLIC_WALLET_CONNECT_ID with the resulting Project ID.

Quick check: Make sure you've updated these values in .env, not .env.sample 🤠

#### 3. Start the frontend

```bash
yarn dev
```

Visit http://localhost:3000/

#### 4. Optional: host your website using Fleek

I've documented a similar hosting process here: https://github.com/oceans404/fullstack-sockets-demo#deploy-your-frontend

## Logic flow

This frontend interacts with the verifier server to

- Watch for events emitted by socket for the user's specific sessionId
  - frontend:
  - backend:
    - getAuthQr in progress
    - getAuthQr done
    - handleVerification in progress
    - handleVerification done
- Request the QR code containing the birthday query (zk request) for display
  - frontend fetch
  - backend getAuthQr
  - backend birthday query
- Report verification result to the rest of the app
