<!-- mcp-name: io.github.byteplant-dev/byteplant-mcp -->
# Byteplant Validator MCP Server
Email, Phone Number, and Address Validation for the Model Context Protocol (MCP)

This package provides an MCP server that uses Byteplant’s Email Validator, Phone Validator, and Address Validator APIs to deliver real-time validation inside any MCP-compatible client.

## Features
- Email validation
- Phone number validation
- Postal address validation
- Fast stdio MCP server
- Local execution
- Easy integration with Claude Desktop

## Requirements
- Python ≥ 3.12
- Byteplant API key (one for each validator, depending which ones you use). [You can register to get one here](https://www.byteplant.com/account/)
- MCP Client (e.g. Claude Desktop)


## MCP Configuration (Claude Desktop)
### 1. Installation
First, install the python module. You can use local installation (like `venv`) or global.
```bash
pip install byteplant-mcp
```
### 2. Configuration
Next, add the MCP server to Claude configuration.
```json
{
	"mcpServers": {
		"byteplant": {
			"command": "path/to/python/installation",
			"args": ["-m", "byteplant-mcp"],
			"env": {
				"EV_TOKEN": "<EMAIL VALIDATOR API TOKEN>",
				"PV_TOKEN": "<PHONE VALIDATOR API TOKEN>",
				"AV_TOKEN": "<ADDRESS VALIDATOR API TOKEN>"
			}
		}
	}
}	
```

## Tools
### 1. `validate_email`
Validates an email address.

**Parameters:**
- `email`: An email address to validate [required]
- `timeout`: timeout in seconds [optional; default 10s, min 5s, max 300s]

### 2. `validate_phone`
Validates a phone number.
**Parameters:**
- `phone`: Phone number to validate [required]
- `code`: Two letter ISO 3166-1 country code [optional; if phone number is in international format, empty string if not specified]
- `locale`: IETF language tag for Geocoding (string) [optional; default 'en-US']
- `mode`: express (static checks only)/extensive (full validation) [optional; default = extensive]
- `timeout`: timeout in seconds (int) [optional; default 10s, min 5s, max 300s]

### 3 `validate_address`
Validates a postal address.
**Paraters:**
- `code`: two-letter ISO 3166-1 country code (string), set to 'XX' for international [required]
- `street_adr`: street/housenumber/building, may include unit/apt etc. (string)[required]
- `street_num`: housenumber/building [optional] (string), housenumber/building can either be part of StreetAddress or be provided separately.
- `additional_info`: building/unit/apt/floor etc. [optional] (string)
- `city`: city or locality (city, district) [optional] (string)
- `postal`: zip/postal code [optional] (string)
- `State`: state/province [optional] (string)
- `geocoding`: enable Geocoding [true|false]; default: false [optional] (bool)
- `locale`: output language for countries with multiple postal languages - use only to translate addresses, always leave empty for address validation [IETF language tag]; default: local language [optional] (string)
- `charset`: output character set [us-ascii|utf-8]; default: 'utf-8' [optional] (string)
- `timeout`: timeout in seconds (int) [optional; default 10s, min 5s, max 300s]

## Environment Variables
- `EV_TOKEN`: Your Email Validator API Token
- `PV_TOKEN`: Your Phone Validator API Token
- `AV_TOKEN`: Your Address Validator API Token
You may use only the tokens for the services you use (e.g. only Email Validator), in that case leave the others tokens empty.

## Contact
- Website: https://www.byteplant.com
- Get your API key: https://www.byteplant.com/account/

- Email: contact@byteplant.com