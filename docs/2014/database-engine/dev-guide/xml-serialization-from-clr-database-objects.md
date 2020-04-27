---
title: 從 CLR 資料庫物件進行 XML 序列化 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- serialization
- XML serialization [CLR integration]
- common language runtime [SQL Server], XML serialization
- XmlSerializer class
ms.assetid: ac84339b-9384-4710-bebc-01607864a344
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 646d15dc3091323e6e7db2af757640122fb2f0fd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62779776"
---
# <a name="xml-serialization-from-clr-database-objects"></a>從 CLR 資料庫物件進行 XML 序列化
  XML 序列化是下列兩種狀況所需的作業：  
  
-   從 Common Language Runtime (CLR) 物件叫用 Web 服務。  
  
-   將使用者定義型別 (UDT) 轉換成 XML。  
  
 叫用 `XmlSerializer` 類別來執行 XML 序列化通常會產生額外的序列化組件，而且此組件會多載進入含有來源組件的專案中。 不過，基於安全性考量，這個多載在 CLR 中已停用。 因此，若要在內部[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]呼叫 web 服務或執行從 UDT 到 XML 的轉換，則必須使用稱為**Sgen**的工具，以產生必要序列化元件的 .NET Framework 來手動建立元件。 叫用 `XmlSerializer` 時，您必須遵循下列步驟，手動建立序列化組件：  
  
1.  執行 .NET Framework SDK 所提供的**Sgen**工具，以建立包含來源元件之 XML 序列化程式的元件。  
  
2.  使用 `CREATE ASSEMBLY` 陳述式，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中註冊已產生的組件。  
  
 如需執行 XML 序列化時可能會收到之錯誤的相關資訊，請參閱下列 Microsoft 支援服務文章：「[無法載入動態產生的序列化元件](https://support.microsoft.com/kb/913668)」。  
  
 如需有關 XMLSerializer 不支援之資料類型的詳細資訊，請參閱 .NET Framework 文件集中的＜.NET Framework 中的 XML 結構描述繫結支援＞。  
  
## <a name="see-also"></a>另請參閱  
 [從 CLR 資料庫物件進行資料存取](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)   
 [CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)  
  
  
