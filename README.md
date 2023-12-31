# Azure DNS Private Resolver

Em seu ambiente pode ser necessário a utilização de zonas de DNS privadas, seja pela necessidade de private endpoints ou por outros motivos. O problema da utilização de zonas privadas, é que por default elas respondem somente a consultas internas no azure e para a resolução de nomes funcionar corretamente é necessário que as vnets de onde vão partir as requisições de resolução de nomes estejam configuradas na blade Virtual network links na Zona DNS.

Caso tenham ambiente hibrido, a resolução de nomes não vai funcionar a partir do ambiente on-premises. Neste momento que o Private DNS Resolver entra em ação.
Este recurso possibilita a resolução de nomes nos dois sentidos, tanto a partir do ambiente on-premises para o Azure, quando no sentido inverso. 

Existe outro método para que a resolução de nomes funcione entre os ambientes, basicamente este método utilizaria servidores DNS com encaminhados configurados em Azure. Vamos falar sobre este método em outro artigo.

Este artigo é baseado na documentação oficial da Microsoft e em experiência com a ferramenta.

Fonte: https://learn.microsoft.com/en-us/azure/dns/dns-private-resolver-overview



## 1 - Inbound endpoints
- O Inbound endpoint habilita a resolução a partir do ambiente on-premises ou de outro local privado;
- Para resolver nomes da sua Zona de DNS privada do Azure, insira o endereço IP do Inbound endpoints no conditional fowarder do servidor de DNS local;

## 2 - Outbound endpoints
- O Outbound enpoint habilita a resolução de nomes através de conditional fowarders do Azure para endereços locais;
- Necessário subnet dedicada para isto;
  
## 3 - Virtual Network Links
- O virtual network link habilita a resolução de nomes para as virtual networks necessárias.

## 4 - Rule Sets
- O RuleSet são grupos de regras de encaminhamento;
- Pode ser aplicado a um ou mais Outbound Endpoints;
- Pode ser lincado com uma ou mais Virtual Networks;

## 5 - DNS Fowarding Rules
- São regras para encaminhamento de consultas;
