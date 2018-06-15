---
title: 資料來源物件 (TMSL) |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1dd73918ca2d52cf38dba74455cf225a8c15ac3e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34045372"
---
# <a name="datasources-object-tmsl"></a>資料來源物件 (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  定義模型將資料加入至模型，或傳遞透過 DirectQuery 模式查詢中的匯入期間所使用的資料來源的連接。  在 DirectQuery 模式的模型只能有一個**DataSource**物件。  
  
 除非您要建立、 取代或改變資料來源物件本身，在您的指令碼 （例如，在資料分割的指令碼） 中參考的任何資料來源必須是現有**DataSource**模型中的物件。  
  
## <a name="object-definition"></a>物件定義  
 所有物件都具有一組常用的屬性，包括名稱、 類型、 描述、 屬性集合，以及註解。 **資料來源**物件也有下列屬性。  
  
 型別  
 DataSource 的類型。 目前，唯一有效的值會是提供者 (1)-正常的連接字串。  
  
 connectionString  
 連接字串至少會指定伺服器和資料庫，但也可以包括支援外部 RDBMS，例如資料提供者或使用者帳戶的其他內容。 這是必要的值。 請參閱[SqlConnectionStringBuilder 類別](https://msdn.microsoft.com/en-us/library/ms254500\(v=vs.110\).aspx)如需詳細資訊，關於 SQL Server 資料庫的連接字串屬性。  
  
 impersonationMode  
 指定 Analysis Services 是否應模擬要求查詢之使用者的身分識別。 這個屬性是數值，指定要用於模擬的認證。 列舉值如下：  
  
-   預設值 (1)-伺服器使用認定為適用於使用模擬內容的模擬方法。  
  
-   ImpersonateAccount (2)-伺服器會使用指定的使用者帳戶。  
  
-   ImpersonateAnonymous (3) 的伺服器會使用匿名使用者帳戶。  此選項則不建議，但有時會在使用 HTTP 存取案例處理驗證的自訂應用程式。  
  
-   (4)-也就是 ImpersonateCurrentUser 伺服器會使用用戶端做為連接的使用者帳戶。  
  
-   ImpersonateServiceAccount (5) 的伺服器會使用該伺服器正在執行做為使用者帳戶。  
  
-   ImpersonateUnattendedAccount (6) – 伺服器會使用自動的使用者帳戶。 這用於在 SharePoint 環境中執行的 Power Pivot 或表格式模型。  
  
 如果 Analysis Services 設定為受信任的委派，DirectQuery 模式中可以使用 impersonateCurrentuser 或  
                      impersonateServiceAccount 如果查詢要求的 Analysis Services 服務帳戶的安全性內容中。 請參閱[設定 Analysis Services 進行 Kerberos 限制委派](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)。  
  
 account  
 用於模擬。 已使用有效的登入的資料庫或 Windows 帳戶的讀取權限的外部資料庫。  
  
 密碼  
 提供帳戶的密碼加密的字串。  
  
 maxConnections  
 在資料來源上同時開啟的連線數目上限。  
  
 isolation  
 隔離使用執行命令時，針對資料來源種類。 有效值是 ReadCommitted （1） 或快照集 (2)。  
  
 timeout  
 整數，指定以秒為單位，針對資料來源執行之命令的逾時。  
  
 提供者  
 選擇性字串，可識別關聯式資料庫中，連接上使用，如果沒有其他方式指定連接字串的 managed 的資料提供者名稱。  
  
## <a name="usage"></a>使用方式  
 **資料來源**物件使用於[Alter 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md)，[建立命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md)， [CreateOrReplace 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md)， [Delete 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md)，[重新整理命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md)，和[MergePartitions 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/mergepartitions-command-tmsl.md)。  
  
 A **DataSource**物件是屬性的模型，但也可以指定為給定模型與資料庫之間的一對一對應的資料庫物件的屬性。  資料分割的 SQL 查詢也指定**DataSource**，只能使用一組縮減的屬性。  
  
 建立時，取代或改變資料來源物件，指定物件定義的所有讀寫屬性。 省略的讀 / 寫屬性會被視為刪除。  
  
## <a name="examples"></a>範例  
 **範例 1** -連線到*FoodMart*上具名執行個體的遠端資料庫*銷售*名為的網路伺服器上*Server01*。  
  
```  
"dataSources": [  
      {  
        "name": "SqlServer Server01 FoodMart",  
        "connectionString": "Provider=SQLNCLI11;Data Source=Server01\Sales;Initial Catalog=Foodmart;Integrated Security=SSPI;Persist Security Info=false",  
        "impersonationMode": "impersonateServiceAccount",  
      }  
]  
```  
  
## <a name="full-syntax"></a>完整語法  
 下面是資料來源物件模型的結構描述表示法。  
  
```  
"dataSources": {  
          "type": "array",  
          "items": {  
            "anyOf": [  
              {  
                "description": "ProviderDataSource object of Tabular Object Model (TOM)",  
                "type": "object",  
                "properties": {  
                  "name": {  
                    "type": "string"  
                  },  
                  "description": {  
                    "type": "string"  
                  },  
                  "type": {  
                    "enum": [  
                      "provider"  
                    ]  
                  },  
                  "connectionString": {  
                    "type": "string"  
                  },  
                  "impersonationMode": {  
                    "enum": [  
                      "default",  
                      "impersonateAccount",  
                      "impersonateAnonymous",  
                      "impersonateCurrentUser",  
                      "impersonateServiceAccount",  
                      "impersonateUnattendedAccount"  
                    ]  
                  },  
                  "account": {  
                    "type": "string"  
                  },  
                  "password": {  
                    "type": "string"  
                  },  
                  "maxConnections": {  
                    "type": "integer"  
                  },  
                  "isolation": {  
                    "enum": [  
                      "readCommitted",  
                      "snapshot"  
                    ]  
                  },  
                  "timeout": {  
                    "type": "integer"  
                  },  
                  "provider": {  
                    "type": "string"  
                  },  
                  "annotations": {  
                    "type": "array",  
                    "items": {  
                      "description": "Annotation object of Tabular Object Model (TOM)",  
                      "type": "object",  
                      "properties": {  
                        "name": {  
                          "type": "string"  
                        },  
                        "value": {  
                          "anyOf": [  
                            {  
                              "type": "string"  
                            },  
                            {  
                              "type": "array",  
                              "items": {  
                                "type": "string"  
                              }  
                            }  
                          ]  
                        }  
                      },  
                      "additionalProperties": false  
                    }  
                  }  
                },  
                "additionalProperties": false  
              }  
            ]  
          }  
        },  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [表格式模型指令碼語言 &#40;TMSL&#41; 參考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [DirectQuery 模式](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [設定 HTTP 存取 Analysis Services 上 Internet Information Services & #40; IIS & #41;8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
  
