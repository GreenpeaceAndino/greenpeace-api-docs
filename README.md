_**Draft doccument**_

# [POST] `/create-donation`
## Schema

| País | Nombre | Tipo | Admite | Condición | Requerido | En conjunto con | Descrición | Ejemplo de uso |
| :-- | -- | -- | -- | -- | -- | -- | -- | -- |
||`donation_type`|`string`|`regular` `oneoff`||`true`|
||`first_name`|`string`||`/^(?=.{2,40}$)[a-zA-Z]+(?:[-' ][a-zA-Z]+)*$/`|`true`|| Admite 1 ó mas palabras y los caracteres `'` `-`|
||`last_name`|`string`||`/^(?=.{2,40}$)[a-zA-Z]+(?:[-' ][a-zA-Z]+)*$/`|`true`|| Admite 1 ó mas palabras y los caracteres `'` `-`|
|**AR**|`document_type`|`string`|`dni` `ci` `lc` `le`||`true`|`document_number`|
|**CH**|`document_type`|`string`|`rut`||`true`|`document_number`|
|**CO**|`document_type`|`string`|`cc` `ce` `pp` `ti` `rc`||`true`|`document_number`|
||`document_number`|`string`|||`true`|`document_type`| Este campo valida el número de documento según el `document_type`||
||`email`|`email`|||`true`|
||`birthdate`|`string`||`/([1-2][0-9]\|[0][1-9]\|[3][0-1])\/([0][1-9]\|[1][0-2])\/[1-9][0-9][0-9]{2}/`|`true`||`DD/MM/YYYY`|`"15/06/1989"`|
||`address_country`|`string`|`argentina` `chile` `colombia`||`true`|
|**AR**|`phone_number`|`string`||`/^[0-9]{8,9}$/`|`true`|| Admite dígitos del 0 al 9. Mínimo 8, máximo 9 carácteres|`"41239876"`|
|**CH**|`phone_number`|`string`||`/9[0-9]{4}[0-9]{4}/`|`true`|| Admite dígitos del 0 al 9 comenzando con el `"9"`. Total 9 carácteres.|`"912398765"`|
|**CO**|`phone_number`|`string`||`/^[0-9]{7,10}$/`|`true`|| Admite dígitos del 0 al 9. Mínimo 7, máximo 10 carácteres|`"9849481"`|
|**AR**|`area_code`|`string`||`/^[0-9]{2,4}$/`|`true`|| Admite dígitos del 0 al 9. Mínimo 2, máximo 4 carácteres|`"1234"`|
|**CH**|`area_code`|`string`||`56`|`true`|| Debe recibir el valor `"56"`|
|**CO**|`area_code`|`string`||`/^[0-9]{3}$/`|`true`|| Admite dígitos del 0 al 9. Máximo 3 carácteres|`"123"`|
|**AR**|`address_state`|`object`|`{code: string\|number, name: string}`||`false`|
|**CH**|`address_state`|`object`|`{code: string\|number, name: string}`||`false`|
|**CO**|`address_state`|`object`|`{code: string\|number, name: string}`||`false`|
||`address_city`|`string`|||`false`|
||`address_street`|`string`|||`false`|
||`address_number`|`string`|||`false`|
||`address_city`|`string`|||`false`|
||`amount`|`number`||`> 1`|`true`|
||`utm_source`|`string`|||`true`|
||`utm_medium`|`string`|||`true`|
||`utm_campaign`|`string`|||`true`|
||`utm_term`|`string`|||`true`|
||`utm_content`|`string`|||`true`|
|**AR**|`payment_method`|`string`|`amex` `visa` `visa_debit` `mastercard` `mastercard_debit` `diners` `cabal` `debcabal` `cmr` `cencosud` `naranja`||`true`|
|**CH**|`payment_method`|`string`|`amex` `visa` `visa_debit` `mastercard` `mastercard_debit` `diners` `magna` `redcompra` `prepago`||`true`|
|**CO**|`payment_method`|`string`|`amex` `visa` `visa_debit` `mastercard` `mastercard_debit` `diners` `codensa` `pse`||`true`|
|**AR**|`payment_document_type`|`string`|`dni` `ci` `lc` `le`||`true`|`document_number`|
|**CH**|`payment_document_type`|`string`|`rut`||`true`|`document_number`|
|**CO**|`payment_document_type`|`string`|`cc` `ce` `pp` `ti` `rc`||`true`|`document_number`|
||`payment_document_number`|`string`|||`true`|`payment_document_type`| Este campo valida el número de documento según el `payment_document_type`||
||`payment_type`|`string`|`credit_card` `bank_account`||`true`|
||`payment_bank_entity_name`|`string`||`payment_type === "bank_account"`|||Es requerido si `payment_type` es igual a `"bank_account"`, de lo contrario es `optional`|`"Banco 1"`|
||`payment_bank_account_type`|`string`|`savings_account` `cheking_account`|`payment_type === "bank_account"`|`false`||**TBD** Es requerido si `payment_type` es igual a `"bank_account"`, de lo contrario es `optional`|`"savings_account"`|
||`payment_bank_account_type`|`string`|`savings_account` `cheking_account`|`payment_type === "bank_account"`|`false`||**TBD** Es requerido si `payment_type` es igual a `"bank_account"`, de lo contrario es `optional`|`"savings_account"`|
||`payment_card_holder_name`|`string`||`payment_type === "credit_card"`|`false`||Es requerido si `payment_type` es igual a `"credit_card"`, de lo contrario es `optional`|`Doe Deer`|
||`payment_card_is_card_holder`|`boolean`||`payment_type === "credit_card"`|`false`||Es requerido si `payment_type` es igual a `"credit_card"`, de lo contrario es `optional`|`Doe Deer`|
||`payment_card_due_date`|`string`||`/^([0][1-9]\|[1][0-2])\/[2-4][0-9]$/`|`true`||`MM/YY`|`"06/26"`|
||`payment_card_token_id`|`string` `number`||`payment_type === "credit_card"`|`false`||Es requerido si `payment_type` es igual a `"credit_card"`, de lo contrario es `optional`|`36376GdgdHdg27`|
||`payment_payer_id`|`string` `number`||`payment_type === "credit_card"`|`false`||Es requerido si `payment_type` es igual a `"credit_card"`, de lo contrario es `optional`|
||`donation_start_date`|`date`|||`true`|
||`donation_end_date`|`date`|||`false`||En el caso de que `donation_type` sea igual a `oneoff` el sistema validara que sea igual a `donation_start_date`, de lo contrario es `null`|
||`payment_gateway_name`|`string`|`mercadopago` `payu` `transbank`||`true`|
|**AR**|`payment_card_id`|`string`||`payment_gateway_name === "mercadopago"`|`true`||Solo es requerido si `payment_gateway_name` es igual a `"mercadopago"`|
|**AR**|`payment_card_issuer_id`|`string`||`payment_gateway_name === "mercadopago"`|`true`||Solo es requerido si `payment_gateway_name` es igual a `"mercadopago"`|
|**AR**|`payment_device_id`|`string`||`payment_gateway_name === "mercadopago"`|`true`||Solo es requerido si `payment_gateway_name` es igual a `"mercadopago"`|
|**CO**|`payment_card_first6`|`string`||`/^[0-9]{6}$/`|`true`||Solo es requerido si `payment_gateway_name` es igual a `"payu"` y `payment_type` es igual a `"credit_card"`. Admite solo `6` dígitos|||`salesforce_campaign_id`|`string` `number`|||`false`|



#### Parameters
| Name | Description | Required |
| :-- | -- | -- |
| | | |

### Chile
#### Request Body
application/json
```json
{
    "amount": 1001,
    "address_country": "chile",
    "address_state": "AT",
    "address_street": "Correa",
    "address_number": 1000,
    "area_code": "56",
    "birthdate": "31/12/1900",
    "document_type": "RUT",
    "document_number": "30.686.957-K",
    "donation_type": "oneoff",
    "donation_start_date": "2012-04-23T18:25:43.511Z",
    "email": "doe.deer@email.org",
    "first_name": "Doe",
    "last_name": "Deer",
    "payment_credit_card_token_id": 4783787529,
    "payment_document_type": "RUT",
    "payment_document_number": "30.686.950-K",
    "payment_due_date": "12/29",
    "payment_first6": "222222",
    "payment_gateway_name": "payu",
    "payment_card_holder_name": "Jhon Doe",
    "payment_is_card_holder": false,
    "payment_method": "amex",
    "phone_number": "94584985498",
    "utm_campaign": "campaign",
    "utm_content": "content",
    "utm_medium": "medium",
    "utm_source": "source",
    "utm_term": "term"
}
```

### Colombia
#### Request Body
```json
{
    "email": "dtovbein@greenpeace.org",
    "donation_type": "oneoff",
    "first_name": "Dan",
    "last_name": "Tovbein",
    "birthdate": "31/12/1900",
    "amount": 1001,
    "document_type": "PP",
    "document_number": "30686222",
    "address_country": "colombia",
    "donation_start_date": "2012-04-23T18:25:43.511Z",
    "address_street": "Correa",
    "address_number": 1000,
    "utm_medium": "medium",
    "utm_source": "source",
    "utm_campaign": "campaign",
    "utm_term": "term",
    "utm_content": "content",
    "payment_document_type": "CC",
    "payment_document_number": "30686957",
    "payment_is_card_holder": false,
    "payment_card_holder_name": "Doe Deer",
    "payment_card_due_date": "12/29",
    "payment_card_token_id": 4783787529,
    "payment_gateway_name": "payu",
    "payment_card_first6": "222222",
    "payment_method": "amex",
    "payment_payer_id": "hf4ry748hdjhjdhj",
    "area_code": "053",
    "phone_number": "94584985498",
    "address_state": "030"
}
```

### Argentina
#### Request Body
```json
{
    "email": "dtovbein@greenpeace.org",
    "donation_type": "oneoff",
    "first_name": "Dan",
    "last_name": "Tovbein",
    "document_type": "DNI",
    "document_number": "30686957",
    "birthdate": "31/12/1900",
    "amount": 1001,
    "address_country": "argentina",
    "donation_start_date": "2012-04-23T18:25:43.511Z",
    "address_street": "Correa",
    "address_number": 1000,
    "utm_medium": "medium",
    "utm_source": "source",
    "utm_campaign": "campaign",
    "utm_term": "term",
    "utm_content": "content",
    "payment_document_type": "LC",
    "payment_document_number": "10020030",
    "payment_card_holder_name": "Doe Deer",
    "payment_due_date": "12/29",
    "payment_is_card_holder": false,
    "payment_credit_card_token_id": 4783787529,
    "payment_gateway_name": "mercadopago",
    "payment_method": "visa_debit",
    "payment_card_id": "873874837387",
    "payment_issuer_id": "23948482",
    "area_code": "053",
    "phone_number": "94584985498"
}
```
#### Responses
| Code | Description |
| :-- | -- |
| `201`  | Created |
