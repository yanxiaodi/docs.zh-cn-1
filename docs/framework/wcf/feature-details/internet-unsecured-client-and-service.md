---
title: 不安全的 Internet 客户端和服务
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 97a10d79-3e7d-4bd1-9a99-fd9807fd70bc
ms.openlocfilehash: 7f4a5fada6c2c17563796ae634ee742285551160
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2018
ms.locfileid: "50181480"
---
# <a name="internet-unsecured-client-and-service"></a>不安全的 Internet 客户端和服务
下图显示了 public、 不安全的 Windows Communication Foundation (WCF) 客户端和服务的示例。  
  
 ![不安全的 Internet 客户端和服务方案](../../../../docs/framework/wcf/feature-details/media/publicunsecured.gif "publicUnsecured")  
  
|特征|描述|  
|--------------------|-----------------|  
|安全模式|无|  
|传输|HTTP|  
|绑定|<xref:System.ServiceModel.BasicHttpBinding> 在代码中，或[ \<basicHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)配置中的元素。|  
|互操作性|与现有的 Web 服务客户端和服务进行互操作|  
|身份验证|无|  
|完整性|无|  
|保密性|无|  
  
## <a name="service"></a>服务  
 下面的代码和配置应独立运行。 执行下列操作之一：  
  
-   使用代码（而不使用配置）创建独立服务。  
  
-   使用提供的配置创建服务，但不定义任何终结点。  
  
### <a name="code"></a>代码  
 下面的代码演示如何创建不安全的终结点。 默认情况下，<xref:System.ServiceModel.BasicHttpBinding> 将安全模式设置为 <xref:System.ServiceModel.BasicHttpSecurityMode.None>。  
  
 [!code-csharp[C_UnsecuredService#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_unsecuredservice/cs/source.cs#1)]
 [!code-vb[C_UnsecuredService#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_unsecuredservice/vb/source.vb#1)]  
  
### <a name="service-configuration"></a>服务配置  
 下面的代码使用配置设置相同的终结点。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <behaviors />  
    <services>  
      <service behaviorConfiguration="" name="ServiceModel.Calculator">  
        <endpoint address="http://localhost/Calculator"   
                  binding="basicHttpBinding"  
                  bindingConfiguration="Basic_Unsecured"   
                  name="BasicHttp_ICalculator"  
                  contract="ServiceModel.ICalculator" />  
      </service>  
    </services>  
    <bindings>  
      <basicHttpBinding>  
        <binding name="Basic_Unsecured" />  
      </basicHttpBinding>  
    </bindings>  
    <client />  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="client"></a>客户端  
 下面的代码和配置应独立运行。 执行下列操作之一：  
  
-   使用代码（和客户端代码）创建独立客户端。  
  
-   创建不定义任何终结点地址的客户端。 而使用将配置名称作为参数的客户端构造函数。 例如：  
  
     [!code-csharp[C_SecurityScenarios#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#0)]
     [!code-vb[C_SecurityScenarios#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#0)]  
  
### <a name="code"></a>代码  
 下面的代码演示一个基本的 WCF 客户端访问不安全终结点。  
  
 [!code-csharp[C_UnsecuredClient#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_unsecuredclient/cs/source.cs#1)]
 [!code-vb[C_UnsecuredClient#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_unsecuredclient/vb/source.vb#1)]  
  
### <a name="client-configuration"></a>客户端配置  
 下面的代码将配置客户端。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <bindings>  
      <basicHttpBinding>  
        <binding name="BasicHttpBinding_ICalculator" >  
          <security mode="None">  
          </security>  
        </binding>  
      </basicHttpBinding>  
    </bindings>  
    <client>  
      <endpoint address="http://localhost/Calculator/Unsecured"  
          binding="basicHttpBinding"   
          bindingConfiguration="BasicHttpBinding_ICalculator"  
          contract="ICalculator"   
          name="BasicHttpBinding_ICalculator" />  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅  
 [常用安全方案](../../../../docs/framework/wcf/feature-details/common-security-scenarios.md)  
 [安全性概述](../../../../docs/framework/wcf/feature-details/security-overview.md)  
 [Windows Server App Fabric 的安全模型](https://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)
