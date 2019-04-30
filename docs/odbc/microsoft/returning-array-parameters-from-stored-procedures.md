---
title: 傳回陣列參數，從預存程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 2018069b-da5d-4cee-a971-991897d4f7b5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a154a8739438b76f12e311d0dec0e9d98d886457
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127993"
---
# <a name="returning-array-parameters-from-stored-procedures"></a>從預存程序傳回陣列參數
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用所提供的 ODBC 驅動程式。  
  
 在 Oracle 7.3 沒有辦法從 PL/SQL 程式存取以外的 PL/SQL 記錄類型。 如果在封裝的程序或函式定義為 PL/SQL 記錄類型的正式引數，它不該做為參數的型式引數繫結。 使用在 Microsoft ODBC Driver for Oracle 的 PL/SQL 資料表型別，可叫用含有正確逸出序列的程序中的陣列參數。  
  
 若要叫用程序，請使用下列語法：  
  
```  
{call  <package-name>.<proc-or-func>;  
(..., {resultset <max-records-requested> ,<formal-array-param_1>,;  
 <formal-array-param_2>,...,<formal-array-param_n> }, ... ) }  
```  
  
> [!NOTE]  
>  \<最大記錄要求 > 參數必須是大於或等於出現在結果集中的資料列數目。 否則，Oracle，就會傳回錯誤驅動程式傳遞給使用者。  
>   
>  PL/SQL 記錄不能做為陣列參數。 每個陣列參數可代表資料庫資料表只有一個資料行。  
  
 下列範例會定義內含傳回不同結果集的兩個程序的封裝，，然後提供兩種方式可從封裝中傳回結果集。  
  
## <a name="package-definition"></a>封裝定義：  
  
```  
CREATE OR REPLACE PACKAGE SimplePackage AS  
  
TYPE t_id is TABLE of  NUMBER(5)  
    INDEX BY BINARY_INTEGER;  
  
TYPE t_Course is TABLE of VARCHAR2(10)  
    INDEX BY BINARY_INTEGER;  
  
TYPE t_Dept is TABLE of VARCHAR2(5)  
    INDEX BY BINARY_INTEGER;  
  
PROCEDURE proc1  
   (  
   o_id             OUT    t_id,  
   ao_course       OUT    t_Course,  
   ao_dept         OUT    t_Dept  
   );  
  
TYPE t_pk1Type1 IS TABLE OF VARCHAR2(100) INDEX BY BINARY_INTEGER;  
TYPE t_pk1Type2 IS TABLE OF NUMBER INDEX BY BINARY_INTEGER;  
PROCEDURE proc2  
   (  
   i_Arg1         IN    NUMBER,  
   ao_Arg2         OUT   t_pk1Type1,  
   ao_Arg3         OUT   t_pk1Type2  
   );  
  
END SimplePackage;  
  
CREATE OR REPLACE PACKAGE BODY SimplePackage AS  
    PROCEDURE  proc1 ( o_id OUT t_id,  
    ao_course OUT t_Course, ao_dept OUT t_Dept   ) AS  
    BEGIN  
          o_id(1):= 200;  
          ao_course(1) :=  'M101';  
          ao_dept(1) :=  'EEE' ;  
  
          o_id(2) := 201;  
          ao_course(2) :=  'PHY320';  
          ao_dept(2) :=  'ECE' ;  
  
     END proc1;  
PROCEDURE proc2  
   (  
   i_Arg1         IN    NUMBER,  
   ao_Arg2         OUT   t_pk1Type1,  
   ao_Arg3         OUT   t_pk1Type2  
   )  
AS  
   i   NUMBER;  
BEGIN  
   FOR i IN 1 .. i_Arg1 LOOP  
      ao_Arg2(i) := 'Row Number ' || to_char(i);  
   END LOOP;  
   FOR i IN 1 .. i_Arg1 LOOP  
      ao_Arg3(i) := i;  
   END LOOP;  
END proc2;  
END SimplePackage;  
```  
  
#### <a name="to-invoke-procedure-proc1"></a>若要叫用程序 PROC1  
  
1.  傳回單一結果集中的所有資料行：  
  
    ```  
    {call SimplePackage.Proc1( {resultset  3, o_id , ao_course, ao_dept  } ) }  
    ```  
  
2.  傳回每個資料行做為單一結果集：  
  
    ```  
    {call SimplePackage.Proc1( {resultset 3, o_id},  {resultset 3, ao_course}, {resultset 3, ao_dept} ) }  
    ```  
  
     這會傳回三個結果集，每個資料行。  
  
#### <a name="to-invoke-procedure-proc2"></a>若要叫用程序 PROC2  
  
1.  傳回單一結果集中的所有資料行：  
  
    ```  
    {call SimplePackage.Proc2( 5 , {resultset  5, ao_Arg2, ao_Arg3} ) }  
    ```  
  
2.  傳回每個資料行做為單一結果集：  
  
    ```  
    {call SimplePackage.Proc2( 5 , {resultset 5, ao_Arg2}, {resultset 5, ao_Arg3} ) }  
    ```  
  
 請確定您的應用程式可以擷取所有結果集使用[SQLMoreResults](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) API。 如需詳細資訊，請參閱*ODBC 程式設計人員參考*。  
  
> [!NOTE]  
>  在 ODBC Driver for Oracle 2.0 版中，Oracle 函數傳回 PL/SQL 陣列不能傳回結果集。
