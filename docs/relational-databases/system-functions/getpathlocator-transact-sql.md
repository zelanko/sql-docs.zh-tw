---
title: GetPathLocator & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- GetPathLocator
- GetPathLocator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetPathLocator function
ms.assetid: 78b7e220-445b-4fdf-811b-7253f4f2b058
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7770ced88953fd64d9ce48b624416b9a7e787f7e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47699126"
---
# <a name="getpathlocator-transact-sql"></a>GetPathLocator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回 FileTable 中指定之檔案或目錄的路徑定位程式識別碼值。  
  
## <a name="syntax"></a>語法  
  
```  
  
GetPathLocator(filenamespace_path)  
```  
  
## <a name="arguments"></a>引數  
 *filenamespace_path*  
 FileTable 中的命名空間路徑。 命名空間路徑的類型是**nvarchar （max)**。  
  
 當資料庫屬於 Alwayson 可用性群組，則**GetPathLocator**函式會接受虛擬網路名稱 (VNN) 或電腦名稱。  
  
## <a name="return-type"></a>傳回類型  
 **hierarchyid**  
  
## <a name="general-remarks"></a>一般備註  
 如需詳細資訊，請參閱 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)。  
  
## <a name="examples"></a>範例  
 您可以使用**GetPathLocator**函式，當您從檔案伺服器的移轉檔案至 FileTable。 在這個案例中，您要將檔案移入 FileTable，然後用 FileTable UNC 路徑取代每個檔案的原始 UNC 路徑。 如需完整範例，請參閱 <<c0> [ 將檔案載入 Filetable](../../relational-databases/blob/load-files-into-filetables.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用 FileTable 中的目錄與路徑](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
