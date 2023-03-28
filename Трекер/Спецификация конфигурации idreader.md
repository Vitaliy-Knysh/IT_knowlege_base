Конфигурация используется для описания требуемого состава и свойств устройства.

Конфигурация является уникальной для отдельного артикула.

### Описание конфигурации

```json
{
  "author": "<str>",
  "revision": "<int>",
  "@timestamp": "<date>",
  
  "device_family": "<str>",
  "device_type": "<str>",
  
  "device_id": {
    "type": "ext",
    "source": "device_id"
  },
  "factory_id": {
    "type": "ext",
    "source": "factory_id"
  },
  
  "components":[
    {
      "type": "device_type_1",
      "PartNumber": "<PartNumber>",
      "amount": "<int>" 
    },
    {
      "type": "device_type_2",
      "PartNumber": "<PartNumber>",
      "amount": "<int>" 
    },
    {
      "type": "device_type_2",
      "PartNumber": "<PartNumber>",
      "amount": "<int>" 
    },
    ...
    {
      "type": "device_type_n",
      "PartNumber": "<PartNumber>",
      "amount": "<int>" 
    }
  ],
  
  "attributes": {
    "MACs": {
      "amount": "<int>",
      "regex": "<regex>"
    }
    "SMBIOS":"<SMBIOS_config>, optional",
    "FRU": "<FRU_config>, optional"
  }
}
```

### Пример конфигурации

```json
{
  "author": "Valeev Timur",
  "revision": 1,
  "@timestamp": "2022-09-08T12:00:00",

  "device_type": "motherboard",
  "device_family": "C624CF",

  "device_id": 
    {
      "type": "ext",
      "source": "device_id"
    },
  "factory_id": 
    {
      "type": "ext",
      "source": "factory_id"
    },

  "components": [
  	{
      "type": "backplane",
      "PartNumber": 10060985,
      "amount": 1
    },
    {
      "type": "motherboard",
      "PartNumber": 10060982,
      "amount": 1
    },
    {
      "type": "riser",
      "PartNumber": 10068182,
      "amount": 2
    },
        {
      "type": "riser",
      "PartNumber": 10068180,
      "amount": 1
    },
        {
      "type": "backplane",
      "PartNumber": 10067655,
      "amount": 1
    },
        {
      "type": "chassis",
      "PartNumber": 10062661,
      "amount": 1
    }
  ],

  "attributes": {
    "MACs": {
      "number": 6,
      "regex": "^00583[fF][0]*[1-9a-fA-F]+[0-9a-fA-F]*$"
  	},
    
  "FRU": {
    "Board": {
      "Manufacturer": "Aquarius",
      "PartNumber": "AQC624CF R30",
      "Product": "AQC624CF",
      "FRUFileID": "AQC624CF rev.1.2a",
      "Serial": {
        "type": "ext",
        "source": "device_id"
      	}
      }
    }
  }
}
```