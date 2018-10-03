---
title: ADO 基本概念 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: d6a66928-e68f-4c38-b87a-838c5de50a28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 448eda8c3c77f410bedd88d1193f2302c926ee95
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47681366"
---
# <a name="ado-fundamentals"></a>ADO 基本概念
ADO 提供開發人員一種功能強大的邏輯物件模型以程式設計方式存取、 編輯和更新資料從各種資料來源，透過系統的 OLE DB 介面。 ADO 的最常見的用法是查詢關聯式資料庫中資料表或資料表，請擷取和結果顯示在應用程式，並可能讓使用者進行變更和儲存的資料。 其他工作包括下列各項：  
  
-   查詢資料庫使用 SQL，並顯示結果。  
  
-   透過網際網路存取的檔案存放區中的資訊。  
  
-   處理郵件與電子郵件系統中的資料夾。  
  
-   將資料從資料庫中儲存成 XML 檔案。  
  
-   執行命令以 XML 描述，並擷取 XML 資料流。  
  
-   將資料儲存到二進位或 XML 資料流。  
  
-   允許使用者檢視及變更資料庫資料表中的資料。  
  
-   建立及重複使用參數化資料庫命令。  
  
-   執行預存程序。  
  
-   以動態方式建立彈性的結構，稱為**資料錄集**保存、 瀏覽，以及操作資料。  
  
-   執行交易式資料庫作業。  
  
-   篩選和排序的執行時間準則為基礎的資料庫資訊的本機複本。  
  
-   建立和管理資料庫中的階層式結果。  
  
-   資料感知元件的繫結資料庫欄位。  
  
-   建立遠端，中斷**資料錄集**。  
  
 ADO 會公開各種不同的選項和設定，以提供這種彈性。 因此，務必了解如何使用 ADO 的應用程式中，然後再細分成容易管理的片段您目標的每個在採取按步就班的方法。  
  
 在大部分使用 ADO 的應用程式牽涉到四個主要作業： 取得資料、 檢查資料、 編輯資料，以及更新資料。 這些作業會檢查在本章節稍後的更多詳細資料。  
  
 不過，我們會討論這些詳細資料之前，我們將提供 ADO 物件模型和簡單的 ADO 應用程式，它以 Microsoft® Visual Basic® 撰寫，並執行每個四個主要的 ADO 作業的概觀：  
  
-   [ADO 物件和集合](../../../ado/guide/data/ado-objects-and-collections.md)  
  
-   [HelloData：簡易 ADO 應用程式](../../../ado/guide/data/hellodata-a-simple-ado-application.md)  
  
-   [OLE DB 提供者](../../../ado/guide/data/ole-db-providers-ado.md)  
  
-   [錯誤](../../../ado/guide/data/errors-ado.md)
