This looks like an Angular application, so I'll guide you through creating something similar from scratch using Angular CLI. Here's a step-by-step approach:

## Step 1: Install Prerequisites

First, make sure you have Node.js and npm installed on your system. Then you can install Angular CLI:

```bash
# Check if Node.js is installed
node -v
npm -v

# Install Angular CLI globally
npm install -g @angular/cli
```

## Step 2: Create a New Angular Project

```bash
# Create a new Angular project
ng new token-creator
cd token-creator
```

When prompted, choose:
- CSS for styling (or SCSS if you prefer)
- Enable Angular routing

## Step 3: Add Required Dependencies

For a DEXTools-like token creator, you'll need several libraries:

```bash
# Install common dependencies for crypto/web3 projects
npm install ethers web3 @angular/material primeng primeicons
```

## Step 4: Set Up Theme System

Create light and dark themes similar to the original:

```bash
# Create theme files
mkdir src/assets/themes
touch src/assets/themes/light.css
touch src/assets/themes/dark.css
```

## Step 5: Create Basic Structure

Update your `app.component.html` and create necessary components:

```bash
# Generate main components
ng generate component header
ng generate component footer
ng generate component token-creator
ng generate component landing-page
```

## Step 6: Set Up Theme Switching

Create a service to handle theme switching:

```bash
ng generate service services/theme
```

Then implement the theme service logic to handle dark/light mode switching similar to what you saw in the original HTML.

## Step 7: Create Root Component Structure

Update `app.component.html` to include header, router outlet, and footer:

```html
<app-header></app-header>
<router-outlet></router-outlet>
<app-footer></app-footer>
```

## Step 8: Add Routing Configuration

Update `app-routing.module.ts` to include routes for your token creator:

```typescript
const routes: Routes = [
  { path: '', component: LandingPageComponent },
  { path: 'create', component: TokenCreatorComponent },
  // Add other routes as needed
];
```

## Step 9: Create the Token Creator Form

Build the token creation form with validation and blockchain integration:

```bash
# Generate form components
ng generate component token-creator/basic-info
ng generate component token-creator/tokenomics
ng generate component token-creator/deployment
```

## Step 10: Add Web3 Integration

Create services for blockchain interaction:

```bash
ng generate service services/web3
ng generate service services/token
```

## Step 11: Test and Build

Test your application locally and build for production:

```bash
# Run development server
ng serve

# Build for production
ng build --configuration production
```

## Step 12: Deploy

Deploy to your preferred hosting service.

Would you like me to elaborate on any specific part of this process? For example, I could provide more detailed code examples for the theme switching functionality, token creation form, or Web3 integration.
Let's build the token creation form step by step:

## 1. First, generate the necessary components

```bash
# Generate main form component
ng generate component token-creator/token-form

# Generate step components
ng generate component token-creator/token-form/basic-info
ng generate component token-creator/token-form/tokenomics
ng generate component token-creator/token-form/advanced-settings
ng generate component token-creator/token-form/review-deploy
```

## 2. Create a form model

First, let's create an interface to define our token data structure. Create a file `src/app/models/token.model.ts`:

export interface TokenFormData {
  // Basic Info
  name: string;
  symbol: string;
  decimals: number;
  totalSupply: string;
  description?: string;
  website?: string;
  
  // Tokenomics
  initialBurn: number;
  taxFeeBuy: number;
  taxFeeSell: number;
  liquidityFee: number;
  marketingFee: number;
  
  // Advanced Settings
  antiBot: boolean;
  maxWalletAmount: string;
  maxTransactionAmount: string;
  enableTrading: boolean;
  lockLiquidity: boolean;
  liquidityLockTime: number;
  
  // Addresses
  marketingWallet: string;
  liquidityWallet: string;
  
  // Network
  network: string;
  router: string;
}

export interface DeploymentResult {
  success: boolean;
  transactionHash?: string;
  contractAddress?: string;
  errorMessage?: string;
}

## 3. Create a token service

Let's create a service to handle token creation functionality. Create a file `src/app/services/token.service.ts`:

import { Injectable } from '@angular/core';
import { BehaviorSubject, Observable, of } from 'rxjs';
import { TokenFormData, DeploymentResult } from '../models/token.model';
import { catchError, delay, tap } from 'rxjs/operators';

@Injectable({
  providedIn: 'root'
})
export class TokenService {
  private tokenFormData = new BehaviorSubject<TokenFormData>({
    name: '',
    symbol: '',
    decimals: 18,
    totalSupply: '1000000',
    description: '',
    website: '',
    
    initialBurn: 0,
    taxFeeBuy: 0,
    taxFeeSell: 0,
    liquidityFee: 0,
    marketingFee: 0,
    
    antiBot: false,
    maxWalletAmount: '0',
    maxTransactionAmount: '0',
    enableTrading: true,
    lockLiquidity: false,
    liquidityLockTime: 0,
    
    marketingWallet: '',
    liquidityWallet: '',
    
    network: 'ethereum',
    router: 'uniswap'
  });

  public currentFormData$ = this.tokenFormData.asObservable();
  
  constructor() { }

  /**
   * Update the token form data
   */
  updateFormData(data: Partial<TokenFormData>): void {
    this.tokenFormData.next({
      ...this.tokenFormData.value,
      ...data
    });
  }
  
  /**
   * Get the current form data
   */
  getFormData(): TokenFormData {
    return this.tokenFormData.value;
  }
  
  /**
   * Reset the form data to default values
   */
  resetFormData(): void {
    this.tokenFormData.next({
      name: '',
      symbol: '',
      decimals: 18,
      totalSupply: '1000000',
      description: '',
      website: '',
      
      initialBurn: 0,
      taxFeeBuy: 0,
      taxFeeSell: 0,
      liquidityFee: 0,
      marketingFee: 0,
      
      antiBot: false,
      maxWalletAmount: '0',
      maxTransactionAmount: '0',
      enableTrading: true,
      lockLiquidity: false,
      liquidityLockTime: 0,
      
      marketingWallet: '',
      liquidityWallet: '',
      
      network: 'ethereum',
      router: 'uniswap'
    });
  }
  
  /**
   * Validate the token data
   */
  validateTokenData(): string[] {
    const errors: string[] = [];
    const data = this.getFormData();
    
    if (!data.name) errors.push('Token name is required');
    if (!data.symbol) errors.push('Token symbol is required');
    if (data.totalSupply === '0') errors.push('Total supply must be greater than 0');
    
    // Add more validation as needed
    
    return errors;
  }
  
  /**
   * Deploy the token to the selected network
   * In a real app, this would connect to Web3 and deploy the contract
   */
  deployToken(): Observable<DeploymentResult> {
    // This is a mock implementation - in real app, you would use web3.js or ethers.js
    const data = this.getFormData();
    
    // Simulate network delay
    return of({
      success: true,
      transactionHash: '0x' + Math.random().toString(16).substr(2, 64),
      contractAddress: '0x' + Math.random().toString(16).substr(2, 40)
    }).pipe(
      delay(3000), // Simulate blockchain delay
      tap(result => console.log('Token deployed:', result)),
      catchError(error => {
        console.error('Deployment error:', error);
        return of({
          success: false,
          errorMessage: 'Failed to deploy token. Please try again.'
        });
      })
    );
  }
  
  /**
   * Generate token contract code preview
   */
  generateContractPreview(): string {
    const data = this.getFormData();
    
    // This is a simplified template - real implementation would be more complex
    return `// SPDX-License-Identifier: MIT
pragma solidity ^0.8.4;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract ${data.name.replace(/\s+/g, '')} is ERC20, Ownable {
    uint256 public taxFeeBuy = ${data.taxFeeBuy};
    uint256 public taxFeeSell = ${data.taxFeeSell};
    uint256 public liquidityFee = ${data.liquidityFee};
    uint256 public marketingFee = ${data.marketingFee};
    
    address public marketingWallet = ${data.marketingWallet || '0x0000000000000000000000000000000000000000'};
    // Additional contract details would be generated here
    
    constructor() ERC20("${data.name}", "${data.symbol}") {
        _mint(msg.sender, ${data.totalSupply} * 10 ** decimals());
        
        // Additional constructor logic would be added here
    }
    
    // Token functions would be generated here based on selected features
}`;
  }
}

## 4. Create the main token form component

Now let's build the main form component that will manage the multi-step process:

import { Component, OnInit } from '@angular/core';
import { TokenService } from '../../services/token.service';
import { TokenFormData } from '../../models/token.model';

@Component({
  selector: 'app-token-form',
  templateUrl: './token-form.component.html',
  styleUrls: ['./token-form.component.css']
})
export class TokenFormComponent implements OnInit {
  currentStep = 1;
  totalSteps = 4;
  loading = false;
  formSubmitted = false;
  deploymentSuccess = false;
  contractAddress = '';
  transactionHash = '';
  
  formData: TokenFormData;
  
  constructor(private tokenService: TokenService) {
    this.formData = this.tokenService.getFormData();
  }

  ngOnInit(): void {
    this.tokenService.currentFormData$.subscribe(data => {
      this.formData = data;
    });
  }
  
  nextStep(): void {
    if (this.currentStep < this.totalSteps) {
      this.currentStep++;
    }
  }
  
  prevStep(): void {
    if (this.currentStep > 1) {
      this.currentStep--;
    }
  }
  
  goToStep(step: number): void {
    if (step >= 1 && step <= this.totalSteps) {
      this.currentStep = step;
    }
  }
  
  updateFormData(data: Partial<TokenFormData>): void {
    this.tokenService.updateFormData(data);
  }
  
  deployToken(): void {
    const errors = this.tokenService.validateTokenData();
    
    if (errors.length > 0) {
      alert('Please fix the following errors:\n' + errors.join('\n'));
      return;
    }
    
    this.loading = true;
    
    this.tokenService.deployToken().subscribe(result => {
      this.loading = false;
      this.formSubmitted = true;
      this.deploymentSuccess = result.success;
      
      if (result.success) {
        this.contractAddress = result.contractAddress || '';
        this.transactionHash = result.transactionHash || '';
      } else {
        alert(result.errorMessage);
      }
    });
  }
  
  resetForm(): void {
    this.tokenService.resetFormData();
    this.currentStep = 1;
    this.formSubmitted = false;
    this.deploymentSuccess = false;
    this.contractAddress = '';
    this.transactionHash = '';
  }
}

## 5. Create the HTML template for the form component

<div class="token-form-container">
  <div class="progress-bar">
    <div class="progress-step" [ngClass]="{'active': currentStep >= 1}" (click)="goToStep(1)">
      <div class="step-number">1</div>
      <div class="step-label">Basic Info</div>
    </div>
    <div class="progress-step" [ngClass]="{'active': currentStep >= 2}" (click)="goToStep(2)">
      <div class="step-number">2</div>
      <div class="step-label">Tokenomics</div>
    </div>
    <div class="progress-step" [ngClass]="{'active': currentStep >= 3}" (click)="goToStep(3)">
      <div class="step-number">3</div>
      <div class="step-label">Advanced Settings</div>
    </div>
    <div class="progress-step" [ngClass]="{'active': currentStep >= 4}" (click)="goToStep(4)">
      <div class="step-number">4</div>
      <div class="step-label">Review & Deploy</div>
    </div>
  </div>

  <div class="form-content">
    <!-- Step 1: Basic Info -->
    <div *ngIf="currentStep === 1">
      <app-basic-info 
        [formData]="formData" 
        (formDataChange)="updateFormData($event)">
      </app-basic-info>
    </div>
    
    <!-- Step 2: Tokenomics -->
    <div *ngIf="currentStep === 2">
      <app-tokenomics 
        [formData]="formData" 
        (formDataChange)="updateFormData($event)">
      </app-tokenomics>
    </div>
    
    <!-- Step 3: Advanced Settings -->
    <div *ngIf="currentStep === 3">
      <app-advanced-settings 
        [formData]="formData" 
        (formDataChange)="updateFormData($event)">
      </app-advanced-settings>
    </div>
    
    <!-- Step 4: Review & Deploy -->
    <div *ngIf="currentStep === 4">
      <app-review-deploy 
        [formData]="formData" 
        (deploy)="deployToken()">
      </app-review-deploy>
    </div>
    
    <!-- Deployment Result -->
    <div *ngIf="formSubmitted" class="deployment-result">
      <div *ngIf="loading" class="loading">
        <div class="spinner"></div>
        <p>Deploying your token to the blockchain...</p>
      </div>
      
      <div *ngIf="!loading && deploymentSuccess" class="success-message">
        <h3>🎉 Congratulations! Your token has been deployed successfully.</h3>
        <div class="contract-details">
          <div class="detail-row">
            <span class="label">Contract Address:</span>
            <span class="value">{{ contractAddress }}</span>
            <button class="copy-btn" (click)="copyToClipboard(contractAddress)">Copy</button>
          </div>
          <div class="detail-row">
            <span class="label">Transaction Hash:</span>
            <span class="value">{{ transactionHash }}</span>
            <button class="copy-btn" (click)="copyToClipboard(transactionHash)">Copy</button>
          </div>
        </div>
        <div class="next-steps">
          <h4>Next Steps</h4>
          <ul>
            <li>Add liquidity to your token</li>
            <li>Add your token to DEXTools</li>
            <li>Create a marketing campaign</li>
          </ul>
        </div>
        <button class="btn primary" (click)="resetForm()">Create Another Token</button>
      </div>
      
      <div *ngIf="!loading && !deploymentSuccess" class="error-message">
        <h3>😢 Deployment Failed</h3>
        <p>There was an error deploying your token. Please try again or contact support.</p>
        <button class="btn primary" (click)="resetForm()">Try Again</button>
      </div>
    </div>
  </div>

  <div class="form-navigation" *ngIf="!formSubmitted">
    <button 
      *ngIf="currentStep > 1" 
      class="btn secondary" 
      (click)="prevStep()">
      Previous
    </button>
    
    <button 
      *ngIf="currentStep < totalSteps" 
      class="btn primary" 
      (click)="nextStep()">
      Next
    </button>
    
    <button 
      *ngIf="currentStep === totalSteps" 
      class="btn primary" 
      (click)="deployToken()"
      [disabled]="loading">
      Deploy Token
    </button>
  </div>
</div>

## 6. Create styles for the form component

.token-form-container {
  max-width: 900px;
  margin: 0 auto;
  padding: 2rem;
  background-color: var(--surface-card);
  border-radius: 10px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
}

/* Progress Bar */
.progress-bar {
  display: flex;
  justify-content: space-between;
  margin-bottom: 2rem;
  position: relative;
}

.progress-bar::before {
  content: '';
  position: absolute;
  top: 18px;
  left: 40px;
  right: 40px;
  height: 2px;
  background-color: var(--surface-border);
  z-index: 1;
}

.progress-step {
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
  z-index: 2;
  cursor: pointer;
}

.step-number {
  width: 36px;
  height: 36px;
  border-radius: 50%;
  background-color: var(--surface-border);
  color: var(--text-color-secondary);
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  margin-bottom: 0.5rem;
  transition: all 0.3s ease;
}

.step-label {
  color: var(--text-color-secondary);
  font-size: 0.875rem;
  transition: all 0.3s ease;
}

.progress-step.active .step-number {
  background-color: var(--primary-color);
  color: #ffffff;
}

.progress-step.active .step-label {
  color: var(--text-color);
  font-weight: bold;
}

/* Form Content */
.form-content {
  min-height: 400px;
  margin-bottom: 2rem;
}

/* Form Navigation */
.form-navigation {
  display: flex;
  justify-content: space-between;
}

/* Buttons */
.btn {
  padding: 0.75rem 1.5rem;
  border-radius: 4px;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.2s ease;
  border: none;
}

.btn.primary {
  background-color: var(--primary-color);
  color: #ffffff;
}

.btn.primary:hover {
  background-color: var(--primary-color-dark);
}

.btn.secondary {
  background-color: transparent;
  border: 1px solid var(--primary-color);
  color: var(--primary-color);
}

.btn.secondary:hover {
  background-color: rgba(var(--primary-color-rgb), 0.1);
}

.btn:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

/* Deployment Result */
.deployment-result {
  text-align: center;
  padding: 2rem;
}

.loading {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.spinner {
  width: 40px;
  height: 40px;
  border: 4px solid rgba(var(--primary-color-rgb), 0.3);
  border-radius: 50%;
  border-top-color: var(--primary-color);
  animation: spin 1s linear infinite;
  margin-bottom: 1rem;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

.success-message {
  color: var(--text-color);
}

.error-message {
  color: var(--error-color);
}

.contract-details {
  background-color: var(--surface-hover);
  padding: 1rem;
  border-radius: 8px;
  margin: 1.5rem 0;
}

.detail-row {
  display: flex;
  align-items: center;
  margin-bottom: 0.5rem;
  font-family: monospace;
}

.detail-row .label {
  min-width: 150px;
  font-weight: bold;
}

.detail-row .value {
  flex: 1;
  word-break: break-all;
  text-align: left;
  padding: 0.5rem;
  background-color: var(--surface-ground);
  border-radius: 4px;
}

.copy-btn {
  padding: 0.25rem 0.5rem;
  margin-left: 0.5rem;
  background-color: var(--surface-card);
  border: 1px solid var(--surface-border);
  border-radius: 4px;
  cursor: pointer;
}

.next-steps {
  text-align: left;
  margin: 1.5rem 0;
}

.next-steps ul {
  padding-left: 1.5rem;
}

.next-steps li {
  margin-bottom: 0.5rem;
}

## 7. Now let's create the individual step components, starting with Basic Info:

import { Component, EventEmitter, Input, OnInit, Output } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';
import { TokenFormData } from '../../../models/token.model';

@Component({
  selector: 'app-basic-info',
  templateUrl: './basic-info.component.html',
  styleUrls: ['./basic-info.component.css']
})
export class BasicInfoComponent implements OnInit {
  @Input() formData!: TokenFormData;
  @Output() formDataChange = new EventEmitter<Partial<TokenFormData>>();
  
  basicInfoForm!: FormGroup;
  
  networkOptions = [
    { label: 'Ethereum', value: 'ethereum' },
    { label: 'Binance Smart Chain', value: 'bsc' },
    { label: 'Polygon', value: 'polygon' },
    { label: 'Arbitrum', value: 'arbitrum' },
    { label: 'Optimism', value: 'optimism' }
  ];
  
  routerOptions = [
    { label: 'Uniswap', value: 'uniswap' },
    { label: 'PancakeSwap', value: 'pancakeswap' },
    { label: 'SushiSwap', value: 'sushiswap' }
  ];
  
  constructor(private fb: FormBuilder) { }

  ngOnInit(): void {
    this.initForm();
    
    // Update router options based on selected network
    this.basicInfoForm.get('network')?.valueChanges.subscribe(network => {
      switch (network) {
        case 'ethereum':
        case 'arbitrum':
        case 'optimism':
          this.routerOptions = [
            { label: 'Uniswap', value: 'uniswap' },
            { label: 'SushiSwap', value: 'sushiswap' }
          ];
          this.basicInfoForm.patchValue({ router: 'uniswap' });
          break;
          
        case 'bsc':
          this.routerOptions = [
            { label: 'PancakeSwap', value: 'pancakeswap' }
          ];
          this.basicInfoForm.patchValue({ router: 'pancakeswap' });
          break;
          
        case 'polygon':
          this.routerOptions = [
            { label: 'QuickSwap', value: 'quickswap' },
            { label: 'SushiSwap', value: 'sushiswap' }
          ];
          this.basicInfoForm.patchValue({ router: 'quickswap' });
          break;
      }
    });
    
    // Listen for form changes
    this.basicInfoForm.valueChanges.subscribe(values => {
      this.formDataChange.emit(values);
    });
  }
  
  initForm(): void {
    this.basicInfoForm = this.fb.group({
      name: [this.formData.name, [Validators.required, Validators.maxLength(50)]],
      symbol: [this.formData.symbol, [Validators.required, Validators.maxLength(10)]],
      decimals: [this.formData.decimals, [Validators.required, Validators.min(0), Validators.max(18)]],
      totalSupply: [this.formData.totalSupply, [Validators.required, Validators.pattern(/^\d+$/)]],
      description: [this.formData.description],
      website: [this.formData.website, Validators.pattern(/^(https?:\/\/)?(www\.)?[a-zA-Z0-9]+(\.[a-zA-Z]{2,})+.*$/)],
      network: [this.formData.network, Validators.required],
      router: [this.formData.router, Validators.required]
    });
  }
  
  get nameControl() { return this.basicInfoForm.get('name'); }
  get symbolControl() { return this.basicInfoForm.get('symbol'); }
  get decimalsControl() { return this.basicInfoForm.get('decimals'); }
  get totalSupplyControl() { return this.basicInfoForm.get('totalSupply'); }
  get websiteControl() { return this.basicInfoForm.get('website'); }
}

## 8. Create Basic Info HTML Template

<div class="step-container">
  <h2>Basic Token Information</h2>
  <p class="step-description">
    Enter the basic details for your new token. These properties will be immutable once deployed.
  </p>

  <form [formGroup]="basicInfoForm" class="form-grid">
    <div class="form-group">
      <label for="name">Token Name *</label>
      <input 
        id="name" 
        type="text" 
        formControlName="name" 
        placeholder="e.g. My Awesome Token"
      >
      <div class="error-message" *ngIf="nameControl?.invalid && nameControl?.touched">
        <span *ngIf="nameControl?.errors?.['required']">Token name is required.</span>
        <span *ngIf="nameControl?.errors?.['maxlength']">Token name cannot exceed 50 characters.</span>
      </div>
    </div>

    <div class="form-group">
      <label for="symbol">Token Symbol *</label>
      <input 
        id="symbol" 
        type="text" 
        formControlName="symbol" 
        placeholder="e.g. MAT"
      >
      <div class="error-message" *ngIf="symbolControl?.invalid && symbolControl?.touched">
        <span *ngIf="symbolControl?.errors?.['required']">Token symbol is required.</span>
        <span *ngIf="symbolControl?.errors?.['maxlength']">Token symbol cannot exceed 10 characters.</span>
      </div>
    </div>

    <div class="form-group">
      <label for="decimals">Decimals *</label>
      <input 
        id="decimals" 
        type="number" 
        formControlName="decimals" 
        placeholder="18"
      >
      <div class="error-message" *ngIf="decimalsControl?.invalid && decimalsControl?.touched">
        <span *ngIf="decimalsControl?.errors?.['required']">Decimals is required.</span>
        <span *ngIf="decimalsControl?.errors?.['min'] || decimalsControl?.errors?.['max']">
          Decimals must be between 0 and 18.
        </span>
      </div>
      <div class="form-hint">
        Standard ERC20 tokens use 18 decimals
      </div>
    </div>

    <div class="form-group">
      <label for="totalSupply">Total Supply *</label>
      <input 
        id="totalSupply" 
        type="text" 
        formControlName="totalSupply" 
        placeholder="1000000"
      >
      <div class="error-message" *ngIf="totalSupplyControl?.invalid && totalSupplyControl?.touched">
        <span *ngIf="totalSupplyControl?.errors?.['required']">Total supply is required.</span>
        <span *ngIf="totalSupplyControl?.errors?.['pattern']">
          Total supply must be a whole number.
        </span>
      </div>
    </div>

    <div class="form-group form-group-full">
      <label for="description">Description</label>
      <textarea 
        id="description" 
        formControlName="description" 
        placeholder="Describe your token and its purpose"
        rows="3"
      ></textarea>
    </div>

    <div class="form-group form-group-full">
      <label for="website">Website URL</label>
      <input 
        id="website" 
        type="url" 
        formControlName="website" 
        placeholder="https://yourtokenwebsite.com"
      >
      <div class="error-message" *ngIf="websiteControl?.invalid && websiteControl?.touched">
        <span *ngIf="websiteControl?.errors?.['pattern']">Please enter a valid URL
