---
title: 修改 SQL Server 服務進階屬性使用 VBScript |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- VBScript [WMI]
- modifying SQL Server Service properties
- WMI Provider for Configuration Management, VBScript
ms.assetid: f3c5d981-eaa3-4d34-9b91-37e42636aa81
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 003755ca5366a8571cdcb63f0c59c51a8012bb11
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133395"
---
# <a name="modify-sql-server-service-advanced-properties-using-vbscript"></a>使用 VBScript 修改 SQL Server 服務進階屬性
  本章節描述如何建立 VBScript 程式來列出已安裝的執行個體的版本[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的電腦上執行。  
  
 此程式碼範例會列出在電腦上執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體和它的版本。  
  
### <a name="listing-name-and-version-of-installed-instances-of-sql-server"></a>列出已安裝之 SQL Server 執行個體的名稱和版本  
  
1.  在文字編輯器中開啟新的文件，例如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 記事本。 複製這個程序之後的程式碼，然後使用 .vbs 副檔名來儲存檔案。 此範例稱為 test.vbs。  
  
2.  使用 VBScript `GetObject` 函數連接到電腦管理的 WMI 提供者執行個體。 此範例會連接到名為 mpc 的遠端電腦，但是會省略電腦名稱來連接本機電腦：winmgmts:root\Microsoft\SqlServer\ComputerManagement。 如需有關 `GetObject` 函數的詳細資訊，請參閱 VBScript 參考資料。  
  
3.  使用 `InstancesOf` 方法來列舉服務的清單。 也可以使用簡單 WQL 查詢和 `ExecQuery` 方法 (而不是 `InstancesOf` 方法) 來列舉此服務。  
  
4.  使用 `ExecQuery` 方法和 WQL 查詢來擷取已安裝之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱和版本。  
  
5.  儲存檔案。  
  
6.  輸入執行指令碼`cscript test.vbs`在命令提示字元。  
  
## <a name="example"></a>範例  
  
```  
set wmi = GetObject("WINMGMTS:\\.\root\Microsoft\SqlServer\ComputerManagement12")  
for each prop in wmi.ExecQuery("select * from SqlServiceAdvancedProperty where SQLServiceType = 1 AND PropertyName = 'VERSION'")  
WScript.Echo prop.ServiceName & " " & prop.PropertyName & ": " & prop.PropertyStrValue  
next  
```  
  
  