---
title: "修改 SQL Server 服務進階屬性使用 VBScript |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
dev_langs: VB
helpviewer_keywords:
- VBScript [WMI]
- modifying SQL Server Service properties
- WMI Provider for Configuration Management, VBScript
ms.assetid: f3c5d981-eaa3-4d34-9b91-37e42636aa81
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3c6e29c6279e511fa303b53392f08e10f31b00f5
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="access-wmi-provider-for-configuration-management-using-vbscript"></a>存取使用 VBScript 的組態管理的 WMI 提供者
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]本章節描述如何建立 VBScript 程式來列出已安裝的執行個體的版本[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的電腦上執行。  
  
 此程式碼範例會列出在電腦上執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體和它的版本。  
  
### <a name="listing-name-and-version-of-installed-instances-of-sql-server"></a>列出已安裝之 SQL Server 執行個體的名稱和版本  
  
1.  在文字編輯器中開啟新的文件，例如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 記事本。 複製這個程序之後的程式碼，然後使用 .vbs 副檔名來儲存檔案。 此範例稱為 test.vbs。  
  
2.  使用 VBScript `GetObject` 函數連接到電腦管理的 WMI 提供者執行個體。 此範例會連接到名為 mpc 的遠端電腦，但是會省略電腦名稱來連接本機電腦：winmgmts:root\Microsoft\SqlServer\ComputerManagement。 如需有關 `GetObject` 函數的詳細資訊，請參閱 VBScript 參考資料。  
  
3.  使用 `InstancesOf` 方法來列舉服務的清單。 也可以使用簡單 WQL 查詢和 `ExecQuery` 方法 (而不是 `InstancesOf` 方法) 來列舉此服務。  
  
4.  使用 `ExecQuery` 方法和 WQL 查詢來擷取已安裝之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱和版本。  
  
5.  儲存檔案。  
  
6.  輸入執行指令碼**cscript test.vbs**在命令提示字元。  
  
## <a name="example"></a>範例  
  
```  
set wmi = GetObject("WINMGMTS:\\.\root\Microsoft\SqlServer\ComputerManagement12")  
for each prop in wmi.ExecQuery("select * from SqlServiceAdvancedProperty where SQLServiceType = 1 AND PropertyName = 'VERSION'")  
WScript.Echo prop.ServiceName & " " & prop.PropertyName & ": " & prop.PropertyStrValue  
next  
```  
  
  
