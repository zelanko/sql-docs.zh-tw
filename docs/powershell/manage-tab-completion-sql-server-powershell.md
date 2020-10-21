---
title: 管理完成索引標籤 (SQL Server PowerShell)
description: 了解如何在 SQL Server PowerShell 模組中正確使用三個變數，以控制 Windows PowerShell Tab 鍵自動完成。
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
ms.assetid: 6296848a-890f-4ad3-8d9f-92ed6a79aa00
author: markingmyname
ms.author: maghan
ms.reviewer: matteot, drskwier
ms.custom: ''
ms.date: 10/14/2020
ms.openlocfilehash: d15d859239aa9ea36f0885218d3469489f28a9b2
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "92006089"
---
# <a name="manage-tab-completion-with-sql-server-powershell"></a>使用 SQL Server PowerShell 管理 TAB 鍵自動完成

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 嵌入式管理單元引進三個變數 (**$SqlServerMaximumTabCompletion**、**$SqlServerMaximumChildItems** 及 **$SqlServerIncludeSystemObjects**) 以控制 Windows PowerShell TAB 鍵自動完成功能。 Tab-Completion 透過傳回其名稱開頭為所輸入字串的項目表，來減少必須輸入的資料量。  

[!INCLUDE [sql-server-powershell-version](../includes/sql-server-powershell-version.md)]

如果使用 Windows PowerShell Tab-Completion，當您已輸入一部分的路徑或 Cmdlet 名稱時，可以按 Tab 鍵來取得名稱符合您已輸入之項目的項目清單。 然後您可以從清單中選取想要的項目，而不必輸入名稱的其餘部分。  

如果您正在擁有許多物件的資料庫中工作，TAB 鍵自動完成清單會變得很大。 某些 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 物件類型 (例如檢視表) 也會有大量的系統物件。  

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 嵌入式管理單元引進三個系統變數，可用來控制 TAB 鍵自動完成功能和 **Get-ChildItem**所呈現的資訊量。

## <a name="sqlservermaximumtabcompletion--n"></a>$SqlServerMaximumTabCompletion =** *n*

指定 Tab-Completion 清單中要包含的最大物件數目。 如果您在有 *n* 個物件以上的路徑節點上選取 Tab 鍵，TAB 鍵自動完成清單就會在 *n*處截斷。 *n* 為整數。 預設值為 0，表示列出的物件數沒有限制。  

## <a name="sqlservermaximumchilditems--n"></a>$SqlServerMaximumChildItems =** *n*

指定 **Get-ChildItem**所顯示的最大物件數。 如果 **Get-ChildItem** 在具有 *n* 個物件以上的路徑節點上執行，此清單會在 *n*處截斷。 *n* 為整數。 預設值為 0，表示列出的物件數沒有限制。  

## <a name="sqlserverincludesystemobjects---true--false-"></a>$SqlServerIncludeSystemObjects =** { **$True** | **$False** }

如果設定為 **$True**，表示系統物件是透過 TAB 鍵自動完成功能和 **Get-ChildItem**所顯示。 如果設定為 **$False**，表示未顯示任何系統物件。 預設值為 **$False**。  

## <a name="set-the-sql-server-tab-completion-variables"></a>設定 SQL Server Tab-Completion 變數

針對任何想要變更其預設值的變數，將變數設定為新值。  

### <a name="example-powershell"></a>範例 (PowerShell)

下列範例會設定所有的三個變數，並列出其設定：  

```powershell
$SqlServerMaximumTabCompletion = 20  
$SqlServerMaximumChildItems = 10  
$SqlServerIncludeSystemObjects = $False  
dir variable:sqlserver*  
```

## <a name="see-also"></a>另請參閱

- [安裝 SQL Server PowerShell](download-sql-server-ps-module.md)
- [SQL Server PowerShell](sql-server-powershell.md)