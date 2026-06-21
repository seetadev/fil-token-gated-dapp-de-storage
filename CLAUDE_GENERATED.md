# Claude Generated Code

**Task**: Objective:
Identify and upgrade all outdated dependencies, tools, and configurations in the project, ensuring compatibility and stability

Tasks:

📦 Dependency Upgrades
Check for outdated packages (package.json, requirements.txt, etc.).

Upgrade to latest stable versions.

Flag any breaking changes and suggest necessary code updates.

⚙️ Tooling & Runtime
Review build tools, linters, and runtime environments (e.g., Node.js, Python).

Suggest config updates (e.g., .eslintrc, tsconfig.json) if needed.

🧪 Validation
Ensure changes don’t break the app — suggest or generate tests if applicable.

Recommend manual test areas if automation isn't possible.



**Generated on**: Sat Jul 26 09:41:24 UTC 2025

## Generated Content

```
I'll analyze the codebase and provide a comprehensive upgrade plan to modernize all dependencies, tools, and configurations while ensuring compatibility and stability.

## 📦 Dependency Analysis & Upgrade Plan

### Current Issues Identified:
1. **Capacitor**: Version 5.7.0 → Latest is 6.x
2. **React Router**: Using deprecated v5 → Should upgrade to v6
3. **TypeScript**: Missing explicit version → Should use latest stable
4. **Ethers**: v5.6.0 → Latest is v6.x
5. **MetaMask SDK**: Potentially outdated
6. **Testing**: Missing proper test setup
7. **ESLint**: No configuration file present
8. **Node.js**: Target needs updating

## FILES_TO_CREATE

### 1. `.eslintrc.json`
```json
{
  "extends": [
    "@ionic/eslint-config/recommended",
    "@typescript-eslint/recommended"
  ],
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "ecmaVersion": 2022,
    "sourceType": "module",
    "ecmaFeatures": {
      "jsx": true
    }
  },
  "plugins": ["@typescript-eslint", "react", "react-hooks"],
  "rules": {
    "react-hooks/rules-of-hooks": "error",
    "react-hooks/exhaustive-deps": "warn",
    "@typescript-eslint/no-unused-vars": "warn",
    "@typescript-eslint/no-explicit-any": "warn"
  },
  "env": {
    "browser": true,
    "es2022": true,
    "node": true
  }
}
```

### 2. `.nvmrc`
```
20.11.0
```

### 3. `vitest.config.ts`
```typescript
import { defineConfig } from 'vitest/config';
import react from '@vitejs/plugin-react';

export default defineConfig({
  plugins: [react()],
  test: {
    globals: true,
    environment: 'jsdom',
    setupFiles: ['./src/setupTests.ts'],
    coverage: {
      reporter: ['text', 'json', 'html'],
      exclude: [
        'node_modules/',
        'src/setupTests.ts',
        '**/*.d.ts',
        'src/components/socialcalc/**'
      ]
    }
  }
});
```

### 4. `src/setupTests.ts`
```typescript
import '@testing-library/jest-dom';
import { beforeAll, afterEach, afterAll } from 'vitest';
import { cleanup } from '@testing-library/react';
import { server } from './mocks/server';

// Start server before all tests
beforeAll(() => server.listen({ onUnhandledRequest: 'error' }));

// Clean up after each test case
afterEach(() => {
  cleanup();
  server.resetHandlers();
});

// Close server after all tests
afterAll(() => server.close());
```

### 5. `src/mocks/server.ts`
```typescript
import { setupServer } from 'msw/node';
import { handlers } from './handlers';

// Setup MSW server for API mocking in tests
export const server = setupServer(...handlers);
```

### 6. `src/mocks/handlers.ts`
```typescript
import { rest } from 'msw';

export const handlers = [
  // Mock API handlers for testing
  rest.get('/api/test', (req, res, ctx) => {
    return res(ctx.json({ message: 'test response' }));
  }),
];
```

## FILES_TO_MODIFY

### 1. `package.json`
```json
{
  "name": "GovtInvoiceNew",
  "private": true,
  "version": "0.0.1",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "preview": "vite preview",
    "test.e2e": "cypress run",
    "test.unit": "vitest",
    "test.unit.ui": "vitest --ui",
    "test.unit.coverage": "vitest --coverage",
    "lint": "eslint src --ext ts,tsx --report-unused-disable-directives --max-warnings 0",
    "lint:fix": "eslint src --ext ts,tsx --fix",
    "type-check": "tsc --noEmit",
    "generate-pwa-assets": "pwa-assets-generator",
    "cap:sync": "cap sync",
    "cap:build": "npm run build && cap sync",
    "cap:serve": "cap run ios -l external",
    "cap:open:ios": "cap open ios",
    "cap:open:android": "cap open android"
  },
  "dependencies": {
    "@capacitor/android": "^6.1.2",
    "@capacitor/app": "^6.0.1",
    "@capacitor/core": "^6.1.2",
    "@capacitor/haptics": "^6.0.1",
    "@capacitor/keyboard": "^6.0.2",
    "@capacitor/preferences": "^6.0.2",
    "@capacitor/status-bar": "^6.0.1",
    "@ionic/react": "^8.2.6",
    "@ionic/react-router": "^8.2.6",
    "@metamask/sdk-react": "^0.28.2",
    "@metamask/sdk-react-ui": "^0.28.2",
    "@web3-storage/w3up-client": "^17.1.2",
    "capacitor-email-composer": "^6.0.0",
    "ethers": "^6.13.2",
    "ionicons": "^7.4.0",
    "react": "^18.3.1",
    "react-dom": "^18.3.1",
    "react-router": "^6.26.0",
    "react-router-dom": "^6.26.0"
  },
  "devDependencies": {
    "@capacitor/cli": "^6.1.2",
    "@cypress/vite-dev-server": "^5.1.1",
    "@ionic/eslint-config": "^0.4.0",
    "@testing-library/dom": "^10.4.0",
    "@testing-library/jest-dom": "^6.4.8",
    "@testing-library/react": "^16.0.0",
    "@testing-library/user-event": "^14.5.2",
    "@types/react": "^18.3.3",
    "@types/react-dom": "^18.3.0",
    "@typescript-eslint/eslint-plugin": "^8.0.0",
    "@typescript-eslint/parser": "^8.0.0",
    "@vitejs/plugin-legacy": "^5.4.1",
    "@vitejs/plugin-react": "^4.3.1",
    "@vitest/coverage-v8": "^2.0.5",
    "@vitest/ui": "^2.0.5",
    "cypress": "^13.13.2",
    "eslint": "^9.9.0",
    "eslint-plugin-react": "^7.35.0",
    "eslint-plugin-react-hooks": "^4.6.2",
    "jsdom": "^24.1.1",
    "msw": "^2.3.5",
    "pwa-assets-generator": "^6.3.2",
    "typescript": "^5.5.4",
    "vite": "^5.4.0",
    "vite-plugin-pwa": "^0.20.1",
    "vitest": "^2.0.5"
  },
  "engines": {
    "node": ">=18.0.0",
    "npm": ">=8.0.0"
  }
}
```

### 2. `tsconfig.json`
```json
{
  "compilerOptions": {
    "target": "ES2022",
    "useDefineForClassFields": true,
    "lib": ["DOM", "DOM.Iterable", "ES2022"],
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": false,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "noUncheckedIndexedAccess": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    "forceConsistentCasingInFileNames": true,
    "module": "ESNext",
    "moduleResolution": "Node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx",
    "types": ["vitest/globals", "@testing-library/jest-dom"]
  },
  "include": ["src", "**/*.ts", "**/*.tsx"],
  "exclude": ["node_modules", "dist", "build"],
  "references": [{ "path": "./tsconfig.node.json" }]
}
```

### 3. `tsconfig.node.json`
```json
{
  "compilerOptions": {
    "composite": true,
    "skipLibCheck": true,
    "module": "ESNext",
    "moduleResolution": "Node",
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "target": "ES2022"
  },
  "include": ["vite.config.ts", "vitest.config.ts"]
}
```

### 4. `vite.config.ts`
```typescript
import legacy from "@vitejs/plugin-legacy";
import react from "@vitejs/plugin-react";
import { defineConfig } from "vite";
import { VitePWA } from "vite-plugin-pwa";

export default defineConfig({
  plugins: [
    react(),
    legacy({
      targets: ['defaults', 'not IE 11'],
      modernPolyfills: true,
    }),
    VitePWA({
      registerType: "autoUpdate",
      workbox: {
        globPatterns: ['**/*.{js,css,html,ico,png,svg,woff2}'],
        runtimeCaching: [
          {
            urlPattern: /^https:\/\/fonts\.googleapis\.com\/.*/i,
            handler: 'CacheFirst',
            options: {
              cacheName: 'google-fonts-cache',
              expiration: {
                maxEntries: 10,
                maxAgeSeconds: 60 * 60 * 24 * 365 // 1 year
              }
            }
          }
        ]
      },
      includeAssets: ['favicon.ico', 'apple-touch-icon-180x180.png', 'pwa-512x512.png'],
      manifest: {
        name: 'Government Invoice Suite',
        short_name: 'GovInvoice',
        description: 'Government billing and invoicing application',
        theme_color: '#3880ff',
        background_color: '#ffffff',
        display: 'standalone',
        icons: [
          {
            src: 'pwa-192x192.png',
            sizes: '192x192',
            type: 'image/png'
          },
          {
            src: 'pwa-512x512.png',
            sizes: '512x512',
            type: 'image/png'
          }
        ]
      }
    })
  ],
  build: {
    target: 'es2022',
    sourcemap: true,
    rollupOptions: {
      output: {
        manualChunks: {
          vendor: ['react', 'react-dom'],
          ionic: ['@ionic/react', '@ionic/react-router'],
          socialcalc: ['./src/components/socialcalc/aspiring/SocialCalc.js']
        }
      }
    }
  },
  optimizeDeps: {
    esbuildOptions: {
      target: 'es2022',
      supported: { 
        bigint: true 
      },
    },
    include: ['react', 'react-dom', '@ionic/react']
  },
  esbuild: {
    target: 'es2022',
    supported: {
      bigint: true,
    },
  },
  server: {
    port: 8100,
    host: true
  },
  preview: {
    port: 8080,
    host: true
  }
});
```

### 5. `capacitor.config.ts`
```typescript
import { CapacitorConfig } from '@capacitor/cli';

const config: CapacitorConfig = {
  appId: 'com.government.invoice',
  appName: 'Government Invoice Suite',
  webDir: 'dist',
  server: {
    androidScheme: 'https'
  },
  plugins: {
    SplashScreen: {
      launchShowDuration: 2000,
      launchAutoHide: true,
      backgroundColor: "#3880ff",
      androidSplashResourceName: "splash",
      androidScaleType: "CENTER_CROP",
      showSpinner: false,
      androidSpinnerStyle: "large",
      iosSpinnerStyle: "small",
      spinnerColor: "#999999",
      splashFullScreen: true,
      splashImmersive: true,
      layoutName: "launch_screen",
      useDialog: true,
    },
    StatusBar: {
      style: 'DARK',
      backgroundColor: '#3880ff'
    }
  }
};

export default config;
```

### 6. `src/App.tsx` (Updated for React Router v6)
```tsx
import { IonApp, setupIonicReact } from "@ionic/react";
import { BrowserRouter as Router } from "react-router-dom";
import Home from "./pages/Home";

/* Core CSS required for Ionic components to work properly */
import "@ionic/react/css/core.css";

/* Basic CSS for apps built with Ionic */
import "@ionic/react/css/normalize.css";
import "@ionic/react/css/structure.css";
import "@ionic/react/css/typography.css";

/* Optional CSS utils that can be commented out */
import "@ionic/react/css/padding.css";
import "@ionic/react/css/float-elements.css";
import "@ionic/react/css/text-alignment.css";
import "@ionic/react/css/text-transformation.css";
import "@ionic/react/css/flex-utils.css";
import "@ionic/react/css/display.css";

/* Theme variables */
import "./theme/variables.css";

setupIonicReact();

const App: React.FC = () => (
  <IonApp>
    <Router>
      <Home />
    </Router>
  </IonApp>
);

export default App;
```

### 7. `src/utils/constants.ts` (Updated for Ethers v6)
```typescript
export const MEDT_TOKEN_ADDRESSES = {
  CALIBRATION: "0xb453DA7D84EFE6E235Da083cef89815820dACd85",
  LINEA_SEPOLIA: "",
  BASE_SEPOLIA: "",
  OPTIMISM_SEPOLIA: "",
  POLYGON_AMOY: "",
  CELO_ALFAJORES: ""
} as const;

export const MEDI_INVOICE_ADDRESSES = {
  CALIBRATION: "0xCDE128D0d80d5F108AFCa42CCa81532C0cD215b2",
  LINEA_SEPOLIA: "",
  BASE_SEPOLIA: "",
  OPTIMISM_SEPOLIA: "",
  POLYGON_AMOY: "",
  CELO_ALFAJORES: ""
} as const;

export const SUPPORTED_NETWORKS = {
  CALIBRATION: {
    chainId: "0x4cb2f",
    name: "Filecoin Calibration",
    rpcUrl: "https://api.calibration.node.glif.io/rpc/v1"
  },
  LINEA_SEPOLIA: {
    chainId: "0xe705",
    name: "Linea Sepolia",
    rpcUrl: "https://rpc.sepolia.linea.build"
  },
  BASE_SEPOLIA: {
    chainId: "0x14a34",
    name: "Base Sepolia",
    rpcUrl: "https://sepolia.base.org"
  },
  OPTIMISM_SEPOLIA: {
    chainId: "0xaa37dc",
    name: "Optimism Sepolia", 
    rpcUrl: "https://sepolia.optimism.io"
  },
  POLYGON_AMOY: {
    chainId: "0x13882",
    name: "Polygon Amoy",
    rpcUrl: "https://rpc-amoy.polygon.technology"
  },
  CELO_ALFAJORES: {
    chainId: "0xaef3",
    name: "Celo Alfajores",
    rpcUrl: "https://alfajores-forno.celo-testnet.org"
  }
} as const;

export type NetworkKey = keyof typeof SUPPORTED_NETWORKS;
export type TokenAddress = typeof MEDT_TOKEN_ADDRESSES[NetworkKey];
export type InvoiceAddress = typeof MEDI_INVOICE_ADDRESSES[NetworkKey];
```

### 8. `src/components/Storage/LocalStorage.ts` (Updated types and error handling)
```typescript
import { Preferences } from "@capacitor/preferences";

export class Files {
  created: string;
  modified: string;
  name: string;
  content: string;
  billType: number;

  constructor(
    created: string,
    modified: string,
    content: string,
    name: string,
    billType: number,
  ) {
    this.created = created;
    this.modified = modified;
    this.content = content;
    this.name = name;
    this.billType = billType;
  }

  static create(
    created: string,
    modified: string,
    content: string,
    name: string,
    billType: number = 0,
  ): Files {
    return new Files(created, modified, content, name, billType);
  }
}

export class Local {
  private static readonly FILES_KEY = 'invoice_files';
  private static readonly SETTINGS_KEY = 'app_settings';

  async _saveFile(file: Files): Promise<void> {
    try {
      const existingFiles = await this._getAllFiles();
      const fileIndex = existingFiles.findIndex(f => f.name === file.name);
      
      if (fileIndex >= 0) {
        existingFiles[fileIndex] = file;
      } else {
        existingFiles.push(file);
      }
      
      await Preferences.set({
        key: Local.FILES_KEY,
        value: JSON.stringify(existingFiles)
      });
    } catch (error) {
      console.error('Error saving file:', error);
      throw new Error('Failed to save file');
    }
  }

  async _getFile(fileName: string): Promise<Files | null> {
    try {
      const files = await this._getAllFiles();
      return files.find(f => f.name === fileName) || null;
    } catch (error) {
      console.error('Error getting file:', error);
      return null;
    }
  }

  async _getAllFiles(): Promise<Files[]> {
    try {
      const result = await Preferences.get({ key: Local.FILES_KEY });
      if (!result.value) return [];
      
      const filesData = JSON.parse(result.value);
      return filesData.map((data: any) => 
        new Files(data.created, data.modified, data.content, data.name, data.billType)
      );
    } catch (error) {
      console.error('Error getting all files:', error);
      return [];
    }
  }

  async _deleteFile(fileName: string): Promise<boolean> {
    try {
      const files = await this._getAllFiles();
      const filteredFiles = files.filter(f => f.name !== fileName);
      
      await Preferences.set({
        key: Local.FILES_KEY,
        value: JSON.stringify(filteredFiles)
      });
      
      return true;
    } catch (error) {
      console.error('Error deleting file:', error);
      return false;
    }
  }

  async _clearAllFiles(): Promise<void> {
    try {
      await Preferences.remove({ key: Local.FILES_KEY });
    } catch (error) {
      console.error('Error clearing files:', error);
      throw new Error('Failed to clear files');
    }
  }
}
```

## 🧪 VALIDATION & TESTING

### Create test files for critical components:

### 9. `src/components/Storage/__tests__/LocalStorage.test.ts`
```typescript
import { describe, it, expect, beforeEach, vi } from 'vitest';
import { Preferences } from '@capacitor/preferences';
import { Local, Files } from '../LocalStorage';

vi.mock('@capacitor/preferences');

describe('LocalStorage', () => {
  let storage: Local;

  beforeEach(() => {
    storage = new Local();
    vi.clearAllMocks();
  });

  describe('Files class', () => {
    it('should create a file instance', () => {
      const file = new Files('2024-01-01', '2024-01-01', 'content', 'test.txt', 1);
      
      expect(file.name).toBe('test.txt');
      expect(file.content).toBe('content');
      expect(file.billType).toBe(1);
    });

    it('should create file with static method', () => {
      const file = Files.create('2024-01-01', '2024-01-01', 'content', 'test.txt');
      
      expect(file.billType).toBe(0); // default value
    });
  });

  describe('Local storage operations', () => {
    it('should save and retrieve a file', async () => {
      const mockFile = new Files('2024-01-01', '2024-01-01', 'test content', 'test.txt', 1);
      
      vi.mocked(Preferences.get).mockResolvedValue({ value: null });
      vi.mocked(Preferences.set).mockResolvedValue();

      await storage._saveFile(mockFile);
      
      expect(Preferences.set).toHaveBeenCalledWith({
        key: 'invoice_files',
        value: JSON.stringify([mockFile])
      });
    });

    it('should handle errors when saving file', async () => {
      const mockFile = new Files('2024-01-01', '2024-01-01', 'test content', 'test.txt', 1);
      
      vi.mocked(Preferences.get).mockRejectedValue(new Error('Storage error'));

      await expect(storage._saveFile(mockFile)).rejects.toThrow('Failed to save file');
    });
  });
});
```

## INSTRUCTIONS

### Step-by-Step Upgrade Process:

1. **Backup Current Project**
   ```bash
   git add . && git commit -m "Backup before major upgrades"
   ```

2. **Update Node.js Version**
   ```bash
   # If using nvm
   nvm install 20.11.0
   nvm use 20.11.0
   ```

3. **Remove Old Dependencies**
   ```bash
   rm -rf node_modules package-lock.json yarn.lock
   ```

4. **Install Updated Dependencies**
   ```bash
   npm install
   ```

5. **Update Capacitor**
   ```bash
   # This will update native platform code
   npx cap sync
   ```

6. **Update Android Gradle Files**
   Update `android/build.gradle`:
   ```gradle
   buildscript {
       ext.kotlin_version = '1.9.10'
       dependencies {
           classpath 'com.android.tools.build:gradle:8.1.1'
           classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
       }
   }
   ```

7. **Run Tests**
   ```bash
   npm run test.unit
   npm run lint
   npm run type-check
   ```

8. **Build and Test**
   ```bash
   npm run build
   npm run preview
   ```

### Breaking Changes to Address:

1. **React Router v6**: Update navigation logic
2. **Ethers v6**: Update Web3 integration code
3. **Capacitor v6**: Update plugin usage
4. **TypeScript strict mode**: Fix type issues

### Manual Testing Areas:

1. **Spreadsheet functionality** - Core SocialCalc integration
2. **File saving/loading** - LocalStorage operations
3. **MetaMask integration** - Web3 connectivity
4. **PWA features** - Offline functionality
5. **Mobile platform builds** - iOS/Android compilation
6. **Print functionality** - Native printer integration

### Post-Upgrade Validation:

1. Test all invoice templates load correctly
2. Verify file operations work on mobile devices
3. Confirm Web3 integration functions properly
4. Test PWA offline capabilities
5. Validate print functionality on different platforms

This comprehensive upgrade brings the project to modern standards while maintaining backward compatibility for the core SocialCalc functionality and ensuring government-grade stability and security.
```
