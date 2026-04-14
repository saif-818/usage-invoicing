# Usage-Based Invoicing System

A clean, modular TypeScript (Node.js) console application that reads customer usage data from a JSON file, validates entries, computes charges, and prints formatted invoices.

## Architecture

| Module | File | Responsibility |
|---|---|---|
| `InputLoader` | `src/InputLoader.ts` | Parses JSON, validates each entry, logs warnings for bad data |
| `InvoiceCalculator` | `src/InvoiceCalculator.ts` | Applies tiered pricing rules, builds `Invoice` objects |
| `InvoicePrinter` | `src/InvoicePrinter.ts` | Formats and prints invoices to console |
| Constants | `src/constants.ts` | All pricing rates in one place |
| Types | `src/types.ts` | Shared TypeScript interfaces |
| Tests | `src/calculator.test.ts` | Unit tests for calculator logic |

## Pricing Rules

- **API Calls**: first 10,000 → $0.01/call; above 10,000 → $0.008/call
- **Storage**: $0.25/GB
- **Compute Time**: $0.05/minute

## Running

> Requires Node.js 18+ and TypeScript 5+ (`npm install -g typescript` if not installed).

```bash
# 1. Compile
tsc

# 2. Run with default usage-data.json in project root
node dist/index.js

# 3. Run with a custom file path (bonus feature)
node dist/index.js /path/to/your/usage-data.json

# 4. Run unit tests
node dist/calculator.test.js
```

## Validation Rules

An entry is skipped (with a console warning) if:
- `CustomerId` is missing, null, or not a non-empty string
- Any of `API_Calls`, `Storage_GB`, `Compute_Minutes` is missing, null, not a number, or negative
