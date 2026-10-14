# IRIS Pay OpenCart Extension

This extension integrates IRIS Pay (Open Banking) into your OpenCart store.

 **OpenCart 3.x** (3.0.3.1+) 

---

## Installation

### Option A: Via OpenCart Installer (Recommended)

1. Build the ZIP file:
   - **Windows**: Run `build.ps1` from the root of this repository:
     ```powershell
     powershell -ExecutionPolicy Bypass -File build.ps1
     ```
   - **Linux / macOS**: Run `./build.sh`
   - This generates `irispay.ocmod.zip`.
2. Go to **Admin → Extensions → Installer**.
3. Click **Upload** and select `irispay.ocmod.zip`.

### Option B: Manual Upload

Copy the contents of the `upload/` folder directly into the root of your OpenCart installation on the server:

**OpenCart 3.x (this branch):**
```
upload/
├── admin/controller/payment/irispay.php
├── admin/language/en-gb/payment/irispay.php
├── admin/language/bg-bg/payment/irispay.php
├── admin/view/template/payment/irispay.tpl
├── catalog/controller/payment/irispay.php
├── catalog/language/en-gb/payment/irispay.php
├── catalog/language/bg-bg/payment/irispay.php
├── catalog/model/payment/irispay.php
└── catalog/view/theme/default/template/payment/irispay.tpl
```

---

## Enabling the Extension

1. Go to **Admin → Extensions → Extensions**.
2. Select **Payments** from the dropdown.
3. Find **IRIS Pay** and click the green **Install** (+) button.
4. Click the **Edit** (pencil) button to configure the module.

---

## Configuration

| Setting | Description |
|---|---|
| **API Key** | The API Key provided by IRIS Pay |
| **Environment** | `Sandbox` for testing, `Live` for real payments |
| **SDK Version** | `Production` (Iris Pay) or `Developer` (Infn Dev) |
| **Order Status** | The order status to set when payment is confirmed |
| **Status** | Enable or disable the payment method |
| **Sort Order** | Display order on checkout |

---

## Custom Checkout Modules

### TK Checkout

In the TK Checkout settings, **IRIS Pay must be set to open in a popup**.

After the customer confirms the order, the customer has to choose a bank and approve the payment in the IRIS Pay component. In popup mode TK Checkout shows that component in the popup. Without the popup, TK Checkout hides the payment method's content behind an overlay and only clicks its confirm button. That works for methods such as Cash On Delivery, but the IRIS Pay component stays hidden and the payment cannot be completed.

---

## Webhook Setup

The webhook URL is automatically generated and sent to the IRIS Pay backend when a payment is initiated. No manual configuration is needed in OpenCart.

If required by IRIS Pay Portal:
1. The webhook URL format is:
   ```
   https://yourstore.com/index.php?route=payment/irispay/webhook&state=oc_cart_{ORDER_ID}_{TIMESTAMP}
   ```
2. Log in to your **IRIS Pay Portal** and paste the URL in the Webhook settings.

---

## Features

- Seamless integration with OpenCart 3.x checkout.
- Automatic order status updates via webhooks.
- Real-time payment status polling (every 3 seconds).
- Fallback background polling after 10 seconds.
- postMessage support for SDK iframe events.
- Sandbox / Live environment switching.
- Bulgarian and English admin interface.

---

## Support

For technical support or issues, please contact the IRIS Pay development team.
