# web3-medical-invoice
Web3 Medical Invoice
## Prerequisites

Ensure you have the following installed on your machine:

- Node.js
- Yarn

You can check their versions using the following commands:

```bash
node -v
yarn -v
```

## Getting Started

### Cloning the Repository

Clone your fork of the ZKMedical-Billing repository:

```bash
git clone https://github.com/[USER_NAME]/ZKMedical-Billing/
```

### Navigate to the Project Directory

Change into the `medical-invoice-ionic-tokengated/` directory:

```bash
cd ZKMedical-Billing/medical-invoice-ionic-tokengated/
```

### Opening the Project

Open the project in your preferred code editor. For Visual Studio Code, use:

```bash
code .
```

### Setting Up Environment Variables

1. Create a `.env` file in the root directory:

   ```bash
   touch .env
   ```

2. Copy the contents from `.env.example` and paste them into `.env`.

3. Obtain the following credentials:
   - **Infura API Key:** Visit the [Infura Dashboard](https://app.infura.io/) to create an API key and add it to `.env`:

     ```
     VITE_INFURA_API_KEY=<your_infura_api_key>
     ```

4. Navigate to the [web3-tools-contracts](https://github.com/seetadev/ZKMedical-Billing/tree/main/web3-tools-contracts) directory to get the latest deployed contract address on all supported chains. Update the contract addresses in the `.env` file:

     ```
     VITE_MEDI_INVOICE_CONTRACT_ADDRESS=<contract_address>
     ```

### Installing Dependencies

Install the necessary dependencies using Yarn:

```bash
yarn
```

### Running the Application

#### Serve the Application (Web Version)

Start the web application:

```bash
ionic serve
```

#### Running on Android Device

1. Sync the Android codebase:

   ```bash
   ionic cap sync android
   ```

2. Run the synced APK on an Android device:

   ```bash
   npx cap run android
   ```

3. Open the project in Android Studio:

   ```bash
   ionic cap open android
   ```

#### Running on iOS Device

1. Sync the iOS codebase:

   ```bash
   ionic cap sync ios
   ```

2. Run the synced IPA on an iOS device:

   ```bash
   npx cap run ios
   ```

3. Open the project in Xcode:

   ```bash
   ionic cap open ios
   ```


### Storacha/IPFS

1. Setup your Storacha client by giving your email, it'll send an authorization mail where you have to validate the req
   ![image](https://github.com/user-attachments/assets/c7a2f169-c470-4f09-b57e-e6138c2410de)

2. Modify any content on the spreadsheet and Save the file using saveAs, yyou'll get your CID that is uploaded to your storacha space which is created automatically when you do 1st step
   ![image](https://github.com/user-attachments/assets/b67a39b3-08d2-4d4c-bc69-789d16345e81)

3. Check your Storacha console for the files that are being uploaded
   ![image](https://github.com/user-attachments/assets/53a9d0bf-847b-48a0-9bbf-d28ac2c1d67c)

4. When file uploads are done you can try refreshing for retrieving the files at IPFS files section
   ![image](https://github.com/user-attachments/assets/b0e90e34-d781-41a0-ae31-b576bbabea55)

5. And then you can move these files to the Local storage
   ![image](https://github.com/user-attachments/assets/4215d42b-41ad-43f4-8e4d-ea277ff79bc1)



