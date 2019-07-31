---
ms.openlocfilehash: 327fd6bac9bc1036a0dd07f7b955ee92cb7e40c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68223546"
---
  從 SQL Server 2005 開始，結構描述的行為已經變更。 結果是，假設結構描述相當於資料庫使用者的程式碼可能不會傳回正確的結果。 不應該在曾經使用下列任何一個 DDL 陳述式的資料庫中使用舊目錄檢視 (包括 sysobjects)：CREATE SCHEMA、ALTER SCHEMA、DROP SCHEMA、CREATE USER、ALTER USER、DROP USER、CREATE ROLE、ALTER ROLE、DROP ROLE、CREATE APPROLE、ALTER APPROLE、DROP APPROLE、ALTER AUTHORIZATION。 在此類資料庫中，必須改用新的目錄檢視。 新的目錄檢視會考量 SQL Server 2005 中所導入的主體和結構描述的分隔。 如需目錄檢視的詳細資訊，請參閱[目錄檢視 &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/catalog-views-transact-sql.md)。
   