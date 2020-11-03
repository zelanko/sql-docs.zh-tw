---
description: 連線至 SQL Server 或 Azure SQL Database
title: 連線至 SQL Server 或 Azure SQL Database
ms.custom: seo-lt-2019
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 9803a8a0-a8f1-4b65-87b8-989b06850194
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bd161a78bb0b5249d0ce6f802760acd2048014f6
ms.sourcegitcommit: 67befbf7435f256e766bbce6c1de57799e1db9ad
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/24/2020
ms.locfileid: "92523965"
---
# <a name="connect-to-a-sql-server-or-azure-sql-database"></a>連線至 SQL Server 或 Azure SQL Database

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
若要使用伺服器或資料庫，您必須先連線至伺服器。 您可以同時連線至多部伺服器。

[SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md) 支援多種連線類型。 本文詳細說明如何連線至 SQL Server 與 Azure SQL Database (連線至 Azure SQL 單一資料庫或彈性集區)。 如需其他連線選項的詳細資訊，請參閱此頁面底部的[連結](#see-also)。
  
## <a name="connecting-to-a-server"></a>連接至伺服器  

1. 在 **物件總管** ，按一下 [連線] > [資料庫引擎...]。

   ![連線](../media/connect-to-server/connect-db-engine.png)

1. 填寫 [連線至伺服器] 表單，並按一下 [連線]：

   ![連線至伺服器](../media/connect-to-server/connect.png)

1. 若您連線至 Azure SQL Server，系統可能會提示您登入以建立防火牆規則。 按一下 [登入...]\(如果沒有，請跳至步驟 6)

   ![已標註 [登入] 選項的 [新增防火牆規則] 對話方塊螢幕擷取畫面。](../media/connect-to-server/firewall-rule-sign-in.png)

1. 登入成功後，表單會預先填入您的特定 IP 位址。 若您的 IP 位址常常變更，可能會讓其他位址更容易進行存取，因此，請選取最適合您環境的選項。 

   ![已選取 [新增我的用戶端 IP 位址] 選項且已標註 [確定] 選項的 [新增防火牆規則] 對話方塊螢幕擷取畫面。](../media/connect-to-server/new-firewall-rule.png)

1. 若要建立防火牆規則並連線至伺服器，請按一下 [確定]。

1. 成功連線後，伺服器會顯示在 **物件總管** 中：

   ![已連接](../media/connect-to-server/connected.png)

## <a name="next-steps"></a>後續步驟

[設計、建立及更新資料表](../visual-db-tools/design-tables-visual-database-tools.md)

## <a name="see-also"></a>另請參閱

[SQL Server Management Studio (SSMS)](../sql-server-management-studio-ssms.md)  
[下載 SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md)

[Analysis Services (英文)](/analysis-services/instances/connect-from-client-applications-analysis-services)  
[Integration Services](../../integration-services/sql-server-integration-services.md)  
[Reporting Services](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)  
[Azure 儲存體](../f1-help/connect-to-microsoft-azure-storage.md)