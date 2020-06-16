![Terraform Version](https://img.shields.io/badge/tf-%3E%3D0.12.0-blue.svg)

> Note: This module requires Terraform 0.12 or later. For earlier Terraform versions, see [0.11 Configuration Language](https://www.terraform.io/docs/configuration-0-11/index.html).

# terraform-network-example
Example network for reuse in other modules

## Resources

* Virtual network
* Subnets
* Network security group associations

## Usage

```hcl
module "network" {
  source = "github.com/lufussel/terraform-network-example"

  name                = "dev-appgw-vnet"
  location            = var.location
  resource_group_name = azurerm_resource_group.appgw_rg.name
  address_space       = ["10.100.0.0/22"]
  dns_servers         = []
  tags                = var.tags

  subnets = [ 
      {
        subnet_name                      = "web"
        subnet_address_prefix            = "10.100.1.0/24"
        subnet_network_security_group_id = module.web-nsg.id
      }
  ]

}
```

## License

[MIT](LICENSE)
