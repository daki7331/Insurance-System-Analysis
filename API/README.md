# API contracts in the source documents

This index summarizes proposed contracts already described in the supplied Word documents. It is documentation, not an executable OpenAPI specification or evidence of implemented endpoints. See the original documents for full rules and acceptance criteria.

| Contract | Source | Purpose |
| --- | --- | --- |
| `POST /v2/policies/quote` | [Part 1](../Docs/01-policy-price-before-payment.docx), section «Изменения API, состояний и интерфейса» | Calculate and persist the price before payment. Request: `productCode`. Response 200 includes `quoteId`, price components, KZT, timestamps, and `state=ACTIVE`. |
| `POST /v2/policies/confirm` | Part 1, same section | Confirm a saved quote using `quoteId`. First synchronous completion: 201; repeated completed operation: 200; processing: 202. Payment uses the stored amount. |
| `GET /payments/{paymentKey}` | Part 1, section «Восстановление незавершённого оформления»; [Part 2](../Docs/02-registration-failure-compensation.docx), section 8 | Read payment status for reconciliation. A 404 after possible dispatch does not prove there was no debit. |
| `POST /refunds` | Part 2, section 8 | Refund an original successful payment. Request: `originalPaymentKey`, `idempotencyKey`, `reason=REGISTRATION_REJECTED`. First success: 201; repeat: 200 with the same `refundId`. Amount and customer come from the original payment. |
| `GET /wallets/{iin}/transactions` | Part 2, section 8 | Paginated wallet history linking refunds to payments. External access is limited to the wallet owner through Gateway. |
| `POST /policies/{policyNumber}/registration-resolution` | Part 2, section 8.1 | Authorized operator decision with evidence: `REGISTERED` or `REJECTED`. |
| `POST /policies/{policyNumber}/refund-retry` | Part 2, section 8.1 | Authorized retry for `REFUND_REVIEW` using the original refund key. 202 for processing; 200 if already refunded. |

Gateway exposes the versioned quote/confirm routes with the `/insurance/api` prefix. Internal payment and operator routes have their own access restrictions; they are not all public client endpoints.

The documents also describe the existing legacy `POST /policies` issuance flow and the existing ESB `POST /policy` registration integration. The proposed migration retains legacy compatibility temporarily before retiring the old issuance route with 410, subject to the checks specified in Part 1.

No standalone Swagger/OpenAPI export was attached, so none is included.
