---
title: SQLGet數據和塊游標 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- SQLGetData function [ODBC], block cursors
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 12599cdc-7725-4faf-bcae-e163ea0f5851
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b60d7093552b8f1dbed87d9ad8840ddb5a9e0799
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299748"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData 和區塊資料指標
**SQLGetData**對單個行的單個列進行操作,無法從多個行獲取包含數據的陣列。 這是因為**SQLGetData**的主要用途是獲取部分長數據,並且很少或沒有理由一次對多行執行此操作。  
  
 要將**SQLGetData**與區塊游標一起使用,應用程式首先調用**SQLSetPos**將游標定位在一行上。 然後,它為該行中的列調用**SQLGetData。** 但是,此行為是可選的。 要確定驅動程式是否支援將**SQLGetData**與區塊游標一起使用,應用程式使用SQL_GETDATA_EXTENSIONS選項調用**SQLGetInfo。**
