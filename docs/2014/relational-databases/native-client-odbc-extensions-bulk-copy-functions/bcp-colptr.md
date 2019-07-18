---
title: bcp_colptr | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_colptr
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_colptr function
ms.assetid: 02ece13e-1da3-4f9d-b860-3177e43d2471
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 269ab3c748557d1d2870195524310f2371b79c52
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62689145"
---
# <a name="bcpcolptr"></a>bcp_colptr
  將目前副本的程式變數資料位址設定成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_colptr (  
HDBC   
hdbc  
,  
LPCBYTE   
pData  
,  
INT   
idxServerCol  
);  
  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
 *pData*  
 這是要複製之資料的指標。 如果繫結的資料類型是大數值類型 （例如 SQLTEXT 或 SQLIMAGE）， *pData*可以是 NULL。 NULL *pData*表示 long 資料值將會傳送到 SQL Server 中使用的區塊[bcp_moretext](bcp-moretext.md)。  
  
 如果*pData*設為 NULL，而且資料行對應至繫結的欄位不是大數值型別**bcp_colptr**失敗。  
  
 如需有關大數值類型的詳細資訊，請參閱 < [bcp_bind](bcp-bind.md) **。**  
  
 *idxServerCol*  
 這是資料庫資料表中要將資料複製到其中之資料行的序數位置。 資料表中的第一個資料行是資料行 1。 資料行的序數位置由報告[SQLColumns](../native-client-odbc-api/sqlcolumns.md)。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 **Bcp_colptr**函式可讓您變更特定資料行的來源資料的位址，將資料複製到 SQL Server [bcp_sendrow](bcp-sendrow.md)。  
  
 一開始，設定使用者資料的指標呼叫**bcp_bind**。 如果呼叫之間變更的程式變數資料位址**bcp_sendrow**，您可以呼叫**bcp_colptr**來重設資料的指標。 下次呼叫**bcp_sendrow**的呼叫所定址的資料會將傳送**bcp_colptr**。  
  
 必須有個別**bcp_colptr**想要修改的每個資料行資料位址您資料表中的呼叫。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
