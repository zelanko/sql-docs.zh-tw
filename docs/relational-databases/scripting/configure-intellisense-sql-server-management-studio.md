---
title: 設定 IntelliSense (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Options [SQL Server Management Studio], IntelliSense
- modifying IntelliSense options
- IntelliSense [SQL Server], modifying options
ms.assetid: 3ffc9f31-4efa-4c1a-a033-ed1dc48b065f
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8c2d84b09b0026f13ccae0f71696b84da56d8721
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47842606"
---
# <a name="configure-intellisense-sql-server-management-studio"></a>設定 IntelliSense (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  依預設，大部分 [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense 選項都是開啟的。 不過，您可以關閉 IntelliSense 選項，再利用功能表命令或按鍵組合來叫用它。  
  
> [!IMPORTANT]  
>  目前編輯器工作階段中的某些變更不會生效。  您必須開啟新的 Transact-SQL 編輯器工作階段，才能看到變更。
  
### <a name="to-turn-statement-completion-options-off-by-default"></a>預設關閉陳述式完成選項  

> [!NOTE]
> SQL 資料倉儲不支援 IntelliSense。
>
>
  
1.  在 **[工具]** 功能表上，按一下 **[選項]**。  
  
2.  展開 [文字編輯器]，展開 [所有語言]、[Transact-SQL] 或 [XML]，然後按一下 [一般]。  
  
3.  清除您不需要之 [陳述式完成] 選項的核取方塊，再按一下 **[確定]**。  
  
### <a name="to-modify-transact-sql-intellisense-options"></a>修改 Transact-SQL IntelliSense 選項  
  
1.  在 **[工具]** 功能表上，按一下 **[選項]**。  
  
2.  依序展開 [文字編輯器] 和 [Transact-SQL]，然後按一下 [IntelliSense]。  
  
3.  清除您不需要之 [IntelliSense] 選項的核取方塊。  
  
4.  若要變更停用 IntelliSense 功能的指令碼大小，請從 **[最大指令碼大小]** 清單中選取大小。  
  
5.  若要變更套用至完成清單之函數名稱的大小寫，請從 [內建函數名稱的大小寫] 清單中選取大小寫規格。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
