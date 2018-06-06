---
title: 以程式設計方式使用連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- connection managers [Integration Services], programming
ms.assetid: 2686fe84-1ecc-48b8-9160-e7122274bd84
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ab2f56402a7b6a257a464af9093d5f2fb2c84360
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-connection-managers-programmatically"></a>以程式設計方式使用連接管理員
  在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中，當您在受控碼使用連線管理員時，最常呼叫的方法是相關聯之連線管理員類別的 AcquireConnection 方法。 當您撰寫受控碼時，必須呼叫 AcquireConnection 方法才能使用連線管理員的功能。 不論是在指令碼工作、指令碼元件、自訂物件或是自訂應用程式中撰寫 Managed 程式碼，都必須呼叫這個方法。  
  
 若要成功呼叫 AcquireConnection 方法，您必須知道下列問題的答案：  
  
-   **哪些連線管理員從 AcquireConnection 方法傳回受控物件？**  
  
     許多連線管理員都會傳回非受控 COM 物件 (System.__ComObject)，而這些物件無法輕鬆地從受控碼中加以使用。 這些連接管理員的清單包括最常使用的 OLE DB 連接管理員。  
  
-   **對於傳回受控物件的連線管理員而言，其 AcquireConnection 方法會傳回哪些物件？**  
  
     若要將傳回值轉換成適當的類型，您必須了解 AcquireConnection 方法會傳回的物件類型。 例如，當您使用 SqlClient 提供者時，[!INCLUDE[vstecado](../includes/vstecado-md.md)] 連線管理員的 AcquireConnection 方法會傳回開啟的 SqlConnection 物件。 然而，檔案連線管理員的 AcquireConnection 方法只會傳回字串。  
  
 本主題會回答上述隨附於 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 之連接管理員的問題。  
  
## <a name="connection-managers-that-do-not-return-a-managed-object"></a>不會傳回 Managed 物件的連接管理員  
 下表列出從 AcquireConnection 方法傳回原生 COM 物件 (System.__ComObject) 的連線管理員。 這些 Unmanaged 物件無法輕鬆地從 Managed 程式碼中加以使用。  
  
|連接管理員類型|連接管理員名稱|  
|-----------------------------|-----------------------------|  
|ADO|ADO 連接管理員|  
|MSOLAP90|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 連接管理員|  
|EXCEL|Excel 連接管理員|  
|FTP|FTP 連接管理員|  
|HTTP|HTTP 連接管理員|  
|ODBC|ODBC 連接管理員|  
|OLEDB|OLE DB 連接管理員|  
  
 一般而言，您可以從受控碼使用 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 連線管理員連線至 ADO、Excel、ODBC 或 OLE DB 資料來源。  
  
## <a name="return-values-from-the-acquireconnection-method"></a>從 AcquireConnection 方法傳回值。  
 下表列出從 AcquireConnection 方法傳回受管理物件的連線管理員。 這些 Managed 物件可以輕鬆地從 Managed 程式碼中加以使用。  
  
|連接管理員類型|連接管理員名稱|傳回值的類型|其他資訊|  
|-----------------------------|-----------------------------|--------------------------|----------------------------|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|[!INCLUDE[vstecado](../includes/vstecado-md.md)] 連接管理員|**System.Data.SqlClient.SqlConnection**||  
|FILE|檔案連接管理員|**System.String**|檔案的路徑。|  
|FLATFILE|一般檔案連接管理員|**System.String**|檔案的路徑。|  
|MSMQ|MSMQ 連接管理員|**System.Messaging.MessageQueue**||  
|MULTIFILE|多個檔案連接管理員|**System.String**|其中一個檔案的路徑。|  
|MULTIFLATFILE|多個一般檔案連接管理員|**System.String**|其中一個檔案的路徑。|  
|SMOServer|SMO 連線管理員|**Microsoft.SqlServer.Management.Smo.Server**||  
|SMTP|SMTP 連接管理員|**System.String**|例如： `SmtpServer=<server name>;UseWindowsAuthentication=True;EnableSsl=False;`|  
|WMI|WMI 連接管理員|**System.Management.ManagementScope**||  
|SQLMOBILE|SQL Server Compact 連接管理員|**System.Data.SqlServerCe.SqlCeConnection**||  
  
## <a name="see-also"></a>另請參閱  
 [在指令碼工作中連線至資料來源](../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)   
 [在指令碼元件中連線至資料來源](../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)   
 [在自訂工作中連線至資料來源](../integration-services/extending-packages-custom-objects/task/connecting-to-data-sources-in-a-custom-task.md)  
  
  
