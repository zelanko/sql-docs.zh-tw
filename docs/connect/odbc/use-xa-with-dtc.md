---
title: 使用 XA 搭配 Microsoft ODBC Driver for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/04/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver
author: karinazhou
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 03399ea4653df03c873739b24a167d88564c3927
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "76911112"
---
# <a name="using-xa-transactions"></a>使用 XA 交易
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]


## <a name="overview"></a>概觀

從 17.3 版開始的 Microsoft ODBC Driver for SQL Server 可支援在 Windows、Linux 和 Mac 上使用分散式交易協調器 (DTC) 進行 XA 交易。 驅動程式端的 XA 實作可讓用戶端應用程式將序列作業 (例如啟動、認可、復原交易分支等) 傳送至交易管理員 (TM)。 然後，TM 將會根據這些作業，與 Resource Manager (RM) 進行通訊。 如需有關 XA 規格和適用於 DTC 的 Microsoft 實作 (MS DTC) 的詳細資訊，請參閱[運作方式：SQL Server DTC (MSDTC 和 XA 交易)](https://blogs.msdn.microsoft.com/bobsql/2018/01/28/how-it-works-sql-server-dtc-msdtc-and-xa-transactions/) \(英文\)。



## <a name="the-xacallparam-structure"></a>XACALLPARAM 結構

`XACALLPARAM` 結構會定義 XA 交易管理員要求所需的資訊。 其定義如下：

```
typedef struct XACallParam {    
    unsigned int sizeParam;
    int          operation;
    XID          xid;
    int          flags;
    int          status;
    unsigned int sizeData;
    unsigned int sizeReturned;
} XACALLPARAM, *PXACALLPARAM; 
```

*sizeParam*  
`XACALLPARAM` 結構的大小。 這不包括 `XACALLPARAM` 之後的資料大小。

*operation*  
要傳遞至 TM 的 XA 作業。 可能的作業會在 [xadefs](../../connect/odbc/use-xa-with-dtc.md#xadefsh) 中定義。

*xid*  
交易分支識別碼。

*flags*  
與 TM 要求相關聯的旗標。 可能的值會在 [xadefs](../../connect/odbc/use-xa-with-dtc.md#xadefsh) 中定義。

*status*  
從 TM 傳回狀態。 如需可能的傳回狀態，請參閱 [xadefs](../../connect/odbc/use-xa-with-dtc.md#xadefsh) 標頭。

*sizeData*  
`XACALLPARAM` 之後的資料緩衝區大小。 

*sizeReturned*  
所傳回資料的大小。

若要提出 TM 要求，必須使用屬性 _SQL_COPT_SS_ENLIST_IN_XA_ 和 `XACALLPARAM` 物件的指標來呼叫 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 函式。  

```
SQLSetConnectAttr(hdbc, SQL_COPT_SS_ENLIST_IN_XA, param, SQL_IS_POINTER);  // XACALLPARAM *param
```


## <a name="code-sample"></a>程式碼範例 

下列範例示範如何與 TM 通訊以進行 XA 交易，以及如何從用戶端應用程式執行不同的作業。 如果測試是針對 Microsoft SQL Server 執行，則必須正確設定 MS DTC，才能啟用 XA 交易。 您可以在 [xadefs](../../connect/odbc/use-xa-with-dtc.md#xadefsh) 標頭檔中找到 XA 定義。 

```

// XA-DTC.cpp : Defines the entry point for the console application.
//

#include "sqlwindef.h"
#include "xplatsec.h"

#include <sql.h>
#include <sqlext.h>
#include "XaTestRunner.h"

#include <stdio.h>
#include <iostream>
#include <string>
#include <memory>
#include <thread>
#include <chrono>


enum class TestType { Commit, Commit1Phase, Rollback, Recover};

RETCODE GetRowCount(HSTMT hstmt, const std::string tableName, int& count)
{
    char query[256];
    count = 0;
    sprintf_s(query, sizeof(query), "SELECT COUNT(*) FROM %s", tableName.c_str());
    RETCODE rc = SQLExecDirectA(hstmt, (SQLCHAR*)query, SQL_NTS);
    TestRunner::CheckRC(rc, "GetRowCount::SQLExecDirectA", hstmt, SQL_HANDLE_STMT);
    if (!SQL_SUCCEEDED(rc))
    {
        return rc;
    }

    rc = SQLFetch(hstmt);
    TestRunner::CheckRC(rc, "GetRowCount::SQLFetch", hstmt, SQL_HANDLE_STMT);
    if (!SQL_SUCCEEDED(rc))
    {
        return rc;
    }

    rc = SQLGetData(hstmt, 1, SQL_C_LONG, &count, sizeof(count), NULL);
    TestRunner::CheckRC(rc, "GetRowCount::SQLGetData", hstmt, SQL_HANDLE_STMT);

    return rc;
}

bool TestXaRunner(HDBC hdbc, const char* connString, TestType testType, int timeout = 0)
{
    SQLRETURN rc = SQLDriverConnect(hdbc, NULL, (SQLCHAR*)connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);
    TestRunner::CheckRC(rc, "TestXaRunner::Connecting", hdbc, SQL_HANDLE_DBC);
    if (!SQL_SUCCEEDED(rc))
    {
        return false;
    }

    SQLHSTMT hstmt;
    rc = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);
    TestRunner::CheckRC(rc, "TestXaRunner::Alloc statement", hdbc, SQL_HANDLE_DBC);

    const int ROWS_TO_TEST = 10; 
    int rowCount = 0;
    bool result = false;

    if (SQL_SUCCEEDED(rc))
    {        
        std::string tableName;
        auto testRunner = std::make_shared<XaTestRunner>(hdbc);
        testRunner->GetUniqueName(tableName);
        bool isTableCreated = false;
        RETCODE xaStatus = SQL_ERROR;
        bool isTimeoutTest = false;

        XID xid;
        XaTestRunner::GetUniqueXid(xid);

        do
        {            
            if (!(isTableCreated = testRunner->CreateTable(tableName)))
            {
                std::cout << "TestXaRunner::Failed to create table " << tableName.c_str() << std::endl;
                break;
            }

            if (timeout > 0)
            {
                testRunner->SetTimeout(timeout);
                isTimeoutTest = true;
            }

            rc = testRunner->Start(xid, TMNOFLAGS, xaStatus);
            if (SQL_SUCCEEDED(xaStatus))
            {                
                rc = testRunner->ExecuteInsertSequence(tableName, ROWS_TO_TEST, hstmt);
                TestRunner::CheckRC(rc, "TestXaRunner::ExecuteInsertSequence", hstmt, SQL_HANDLE_STMT);

                if (isTimeoutTest)
                {
                    auto timeToSleep = timeout + 5;
                    std::cout << "Sleep for " << timeToSleep << " seconds" << std::endl;
                    std::this_thread::sleep_for(std::chrono::seconds(timeToSleep));
                }

                rc = testRunner->End(xid, TMSUCCESS, xaStatus);
                if (xaStatus < 0)
                {
                    std::cout << "TestXaRunner::XA End failed status=" << xaStatus << std::endl;
                    break;
                }


                switch (testType)
                {
                case TestType::Commit:
                    rc = testRunner->Prepare(xid, xaStatus);
                    if (xaStatus < 0)
                    {
                        std::cout << "TestXaRunner::XA Prepare failed status=" << xaStatus << std::endl;
                    }
                    else
                    {
                        rc = testRunner->Commit(xid, false, xaStatus);
                        if (xaStatus < 0)
                        {
                            std::cout << "TestXaRunner::XA Commit failed status=" << xaStatus << std::endl;
                        }
                    }
                    break;
                case TestType::Commit1Phase:
                    rc = testRunner->Commit(xid, true, xaStatus);
                    if (xaStatus < 0)
                    {
                        std::cout << "TestXaRunner::XA Commit one phase failed status=" << xaStatus << std::endl;
                    }
                    break;
                case TestType::Rollback:
                    rc = testRunner->Rollback(xid, xaStatus);
                    if (xaStatus < 0)
                    {
                        std::cout << "TestXaRunner::XA Rollback failed status=" << xaStatus << std::endl;
                    }
                    break;
                case TestType::Recover:
                    break;
                default:
                    break;
                }
            }
            else
            {
                std::cout << "TestXaRunner::XA Start failed status=" << xaStatus << std::endl;
            }
            
        } while (false);
        
        if (isTimeoutTest)
        {
            result = xaStatus == XAER_NOTA;
            std::cout << "TestXaRunner::TimeoutTest" " xaStatus=" << xaStatus << " test " << (result ? "Succeded" : "Failed") << std::endl;
        }
        else
        {
            auto isCommit = testType == TestType::Commit || testType == TestType::Commit1Phase;

            rc = GetRowCount(hstmt, tableName, rowCount);
            result = (rowCount == (isCommit ? ROWS_TO_TEST : 0)) && SQL_SUCCEEDED(xaStatus);

            std::cout << "TestXaRunner::" << (isCommit ? "Commit" : "Rollback") << " rowCount=" << rowCount << " xaStatus=" << xaStatus << " test " << (result ? "Succeded" : "Failed") << std::endl;
        }
       
        if (isTableCreated)
        {
            testRunner->DropTable(tableName);
        }

        rc = SQLFreeHandle(SQL_HANDLE_STMT, hstmt);
        rc = SQLDisconnect(hdbc);
    }

    return result;
}

bool TestCommit(HDBC hdbc, const char* connectionString)
{
    return TestXaRunner(hdbc, connectionString, TestType::Commit);
}


bool TestCommit1Phase(HDBC hdbc, const char* connectionString)
{
    return TestXaRunner(hdbc, connectionString, TestType::Commit1Phase);
}


bool TestRollback(HDBC hdbc, const char* connectionString)
{
    return TestXaRunner(hdbc, connectionString, TestType::Rollback);
}


bool TestSetTimeout(HDBC hdbc, const char* connectionString)
{
    bool result = false;
    result = TestXaRunner(hdbc, connectionString, TestType::Commit, 2); 
    result = TestXaRunner(hdbc, connectionString, TestType::Rollback, 5); 

    return result;
}

bool TestRecover(HDBC hdbc, const char* connectionString)
{
    SQLRETURN rc = SQLDriverConnect(hdbc, NULL, (SQLCHAR*)connectionString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);
    TestRunner::CheckRC(rc, "TestXaRunner::Connecting", hdbc, SQL_HANDLE_DBC);
    if (!SQL_SUCCEEDED(rc))
    {
        return false;
    }

    const int ROWS_TO_TEST = 10;
    const int transactionCount = 2;
    int rowCount = 0;
    bool result = false;
    std::vector<std::string> tableNames;
    auto testRunner = std::make_shared<XaTestRunner>(hdbc);
    auto numCompletedTransactions = 0;
    RETCODE xaStatus = SQL_ERROR;
    const int sleepTime = 2;

    for (auto tr = 0; tr < transactionCount; tr++)
    {
        std::string tbName;        
        testRunner->GetUniqueName(tbName);
        bool isTableCreated = false;
        RETCODE xaStatus = SQL_ERROR;

        std::cout << "Started transaction " << tr << std::endl;
        do
        {
            if (!(isTableCreated = testRunner->CreateTable(tbName)))
            {
                tableNames.emplace_back("");
                std::cout << "TestRecover::Failed to create table " << tbName.c_str() << std::endl;
                break;
            }
            tableNames.push_back(std::move(tbName));

            XID xid;
            XaTestRunner::GetUniqueXid(xid);
            rc = testRunner->Start(xid, TMNOFLAGS, xaStatus);
            if (xaStatus < 0)
            {
                std::cout << "TestXaRunner::XA Start failed status=" << xaStatus << std::endl;
                break;
            }
            
            rc = testRunner->ExecuteInsertSequence(tableNames[tr], ROWS_TO_TEST);                

            rc = testRunner->End(xid, TMSUCCESS, xaStatus);
            if (xaStatus < 0)
            {
                std::cout << "TestXaRunner::XA End failed status=" << xaStatus << std::endl;                   
                break;
            }

            std::cout << "Completed transaction " << tr << " formatId=" <<xid.formatID <<std::endl;
            numCompletedTransactions++;

            rc = testRunner->Prepare(xid, xaStatus);
            std::cout << "Prepared transaction " << tr << std::endl;

        } while (false);
    }

    std::cout << "Sleep for " << sleepTime << "seconds" << std::endl;
    std::this_thread::sleep_for(std::chrono::seconds(sleepTime));

    std::vector<unsigned char> buff(8092);
    unsigned int buffSize = static_cast<unsigned int>(buff.size());
    testRunner->Recover(TMSTARTRSCAN | TMENDRSCAN, &buff[0], buffSize, xaStatus);
    std::cout << "TestRecover:: After Recover buffSize=" << buffSize << " xaStatus=" << xaStatus << std::endl;
    if (SQL_SUCCEEDED(xaStatus))
    {
        auto numRecoveredTransactions = buffSize / sizeof(XID);        
        std::cout << "TestRecover:: After Recover numRecoveredTransactions=" << numRecoveredTransactions << std::endl;
        result = numCompletedTransactions == numRecoveredTransactions;
        XID* pXid = (XID*)&buff[0];
        for (auto tr = 0; tr < numRecoveredTransactions; tr++, pXid++)
        {
            rc = testRunner->Commit(*pXid, false, xaStatus);
            if (SQL_SUCCEEDED(xaStatus))
            {
                std::cout << "TestRecover::Successfully committed recovered transaction " << tr << " formatId=" << pXid->formatID << std::endl;
            }
            else
            {
                std::cout << "TestRecover::Attempt to commit recovered transaction " << tr << " failed status=" << xaStatus << " formatId=" << pXid->formatID  << std::endl;
            }
        }
    }

    for (const auto& name : tableNames)
    {
        if (!name.empty())
        {
            testRunner->DropTable(name);
        }
    }

    SQLDisconnect(hdbc);
    return result;
}

int main(int argc, char** argv)
{
    const char* pConnStr = "";
    if (argc < 2)
    {
        std::cout << "ERROR: Connection string is not specified" << std::endl;
        return 0;
    }
    else
    {
        pConnStr = argv[1];
        std::cout << "Connection string: " << pConnStr << std::endl;
    }


    SQLHENV henv = NULL;
    SQLHDBC hdbc = NULL;

    std::string connString = pConnStr;
    SQLRETURN rc;

    rc = SQLAllocHandle(SQL_HANDLE_ENV, NULL, &henv);
    TestRunner::CheckRC(rc, "Allocating environment", NULL, 0);

    rc = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER)SQL_OV_ODBC3, 0);

    rc = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);
    TestRunner::CheckRC(rc, "Allocating connection", henv, SQL_HANDLE_ENV);

    bool result;

    result = TestSetTimeout(hdbc, pConnStr);
    result = TestCommit(hdbc, pConnStr);
    result = TestCommit1Phase(hdbc, pConnStr);
    result = TestRollback(hdbc, pConnStr);
    result = TestRecover(hdbc, pConnStr);

    SQLFreeHandle(SQL_HANDLE_DBC, hdbc);
    SQLFreeHandle(SQL_HANDLE_ENV, henv);

    return 0;
}

```

`XATestRunner` 類別會在與伺服器進行通訊時，實作可能的 XA 呼叫。

```

// XATestRunner.cpp : Implemented XA calls to communicate with the server.
//

#include "XaTestRunner.h"

RandomProvider XidMgr::rndPrv;

int XidMgr::GetRandomNumber(int low, int high)
{
    std::mt19937 gen(XidMgr::rndPrv.rd());
    std::uniform_int_distribution<> dis(low, high);
    return dis(gen);
}

void XidMgr::GetRandomBuffer(unsigned char* buffer, unsigned int sizeBuffer)
{
    std::mt19937 gen(XidMgr::rndPrv.rd());
    std::uniform_int_distribution<> dis(0, 0xff);
    for (unsigned int i = 0; i < sizeBuffer; i++)
    {
        buffer[i] = dis(gen);
    }    
}

XaTestRunner::XaTestRunner(HDBC dbc)
             : TestRunner(dbc)
{
}

XaTestRunner::~XaTestRunner()
{
}

void XidMgr::GetUniqueXid(XID& xid)
{
    long formatId = (long)XidMgr::GetRandomNumber(0, 0xffff);
    GetUniqueXid(xid, formatId);
}

void XidMgr::GetUniqueXid(XID& xid, int formatId, unsigned char* globalId, unsigned int sizeGlobalId)
{    
    auto isGlobalIdDefined = globalId != nullptr && sizeGlobalId > 0 && sizeGlobalId <= 64;

    xid.formatID = formatId;
    xid.bqual_length = 64;
    xid.gtrid_length = isGlobalIdDefined ? sizeGlobalId : 64;
    if (!isGlobalIdDefined)
    {
        GetRandomBuffer(&xid.data[0], xid.gtrid_length);
    }
    else
    { 
        memcpy_s(&xid.data[0], sizeof(xid.data), globalId, xid.gtrid_length);
    }

    GetRandomBuffer(&xid.data[xid.gtrid_length], xid.bqual_length);
}

RETCODE XaTestRunner::IssueXaCall(const XID* pXid, int operation, const int flags, unsigned char* buffer, unsigned int& sizeBuffer, RETCODE& xaStatus)
{
    auto sizeLimit = sizeBuffer;
    unsigned int sizeParam = sizeof(XACALLPARAM) + sizeBuffer;
    std::vector<unsigned char> buff(sizeParam);
    PXACALLPARAM param = (PXACALLPARAM)(void*)&buff[0];    
    memset(param, 0, sizeof(XACALLPARAM));
    param->flags = flags;
    param->operation = operation;
    param->sizeParam = sizeParam;
    if (pXid)
    {
        param->xid = *pXid;
    }
    if (sizeBuffer > 0)
    {
        param->sizeData = sizeBuffer;
        memcpy_s(&param[1], sizeBuffer, buffer, sizeBuffer);
    }

    RETCODE rc = SQLSetConnectAttr(hdbc, SQL_COPT_SS_ENLIST_IN_XA, param, SQL_IS_POINTER);
    CheckRC(rc, " XaTestRunner::IssueXaCall", hdbc, SQL_HANDLE_DBC);
    xaStatus = SQL_SUCCEEDED(rc) ? param->status : rc;
    sizeBuffer = param->sizeReturned;
    if (sizeBuffer)
    {
        memcpy_s(buffer, sizeLimit, &param[1], sizeBuffer);
    }

    return rc;

}

RETCODE XaTestRunner::Start(const XID& xid, const int flags, RETCODE& xaStatus)
{
    unsigned int sizeBuffer = 0;
    return IssueXaCall(&xid, OP_START, flags, nullptr, sizeBuffer, xaStatus);
}

RETCODE XaTestRunner::End(const XID& xid, const int flags, RETCODE& xaStatus)
{
    unsigned int sizeBuffer = 0;
    return IssueXaCall(&xid, OP_END, flags, nullptr, sizeBuffer, xaStatus);
}

RETCODE XaTestRunner::Prepare(const XID& xid, RETCODE& xaStatus)
{
    unsigned int sizeBuffer = 0;
    return IssueXaCall(&xid, OP_PREPARE, TMNOFLAGS, nullptr, sizeBuffer, xaStatus);
}

RETCODE XaTestRunner::Commit(const XID& xid, const bool onePhase, RETCODE& xaStatus)
{
    unsigned int sizeBuffer = 0;
    return IssueXaCall(&xid, OP_COMMIT, onePhase ? TMONEPHASE : TMNOFLAGS, nullptr, sizeBuffer, xaStatus);
}

RETCODE XaTestRunner::Rollback(const XID& xid, RETCODE& xaStatus)
{
    unsigned int sizeBuffer = 0;
    return IssueXaCall(&xid, OP_ROLLBACK, TMNOFLAGS, nullptr, sizeBuffer, xaStatus);
}

RETCODE XaTestRunner::Forget(const XID& xid, RETCODE& xaStatus)
{
    unsigned int sizeBuffer = 0;
    return IssueXaCall(&xid, OP_FORGET, TMNOFLAGS, nullptr, sizeBuffer, xaStatus);
}

RETCODE XaTestRunner::Recover(const int flags, unsigned char* buffer, unsigned int& sizeBuffer, RETCODE& xaStatus)
{
    return IssueXaCall(nullptr, OP_RECOVER, flags, buffer, sizeBuffer, xaStatus);    
}

void XaTestRunner::SetTimeout(const int tmo)
{
    int timeout = tmo;
    unsigned int sizeBuffer = sizeof(timeout);
    RETCODE xaStatus;
    IssueXaCall(nullptr, OP_SETTIMEOUT, TMNOFLAGS, (unsigned char*)&timeout, sizeBuffer, xaStatus);
}

int XaTestRunner::GetTimeout()
{
    int timeout = 0;
    unsigned int sizeBuffer = sizeof(timeout);
    RETCODE xaStatus;
    IssueXaCall(nullptr, OP_GETTIMEOUT, TMNOFLAGS, (unsigned char*)&timeout, sizeBuffer, xaStatus);
    return timeout;
}

void XaTestRunner::XidShortToXid(const XID_SHORT& xids, XID& xid)
{
    xid.formatID = xids.formatID;
    xid.gtrid_length = xids.gtrid_length;
    xid.bqual_length = xids.bqual_length;
    memcpy_s(&xid.data[0], sizeof(xid.data), &xids.data[0], sizeof(xids.data));
}


```


## <a name="appendix"></a>附錄

### <a name="xadefsh"></a>xadefs.h

```
// xadefs.h : XA specific definitions.
//

#pragma once

// from xa.h
/*
 * Transaction branch identification: XID and NULLXID:
 */
#define XIDDATASIZE     128         /* size in bytes */
#define MAXGTRIDSIZE    64          /* maximum size in bytes of gtrid */
#define MAXBQUALSIZE    64          /* maximum size in bytes of bqual */

#ifndef _XID_T_DEFINED
#define _XID_T_DEFINED
struct xid_t
{
    int formatID;                   /* format identifier */
    int gtrid_length;               /* value not to exceed 64 */
    int bqual_length;               /* value not to exceed 64 */
    unsigned char data[XIDDATASIZE];
};
#endif

#pragma pack (push, 1)
struct xid_s
{
    int formatID;                           /* format identifier */
    unsigned char gtrid_length;             /* value not to exceed 64 */
    unsigned char bqual_length;             /* value not to exceed 64 */
    unsigned char data[XIDDATASIZE];
};
#pragma pack (pop)

/*
 * xa_() return codes (resource manager reports to transaction manager)
 */
#define XA_RBBASE       100                 /* The inclusive lower bound of the rollback codes */
#define XA_RBROLLBACK   XA_RBBASE           /* The rollback was caused by an unspecified reason */
#define XA_RBCOMMFAIL   XA_RBBASE+1         /* The rollback was caused by a communication failure */
#define XA_RBDEADLOCK   XA_RBBASE+2         /* A deadlock was detected */
#define XA_RBINTEGRITY  XA_RBBASE+3         /* A condition that violates the integrity of the resources was detected */
#define XA_RBOTHER      XA_RBBASE+4         /* The resource manager rolled back the transaction branch for a reason not on this list */
#define XA_RBPROTO      XA_RBBASE+5         /* A protocol error occurred in the resource manager */
#define XA_RBTIMEOUT    XA_RBBASE+6         /* A transaction branch took too long */
#define XA_RBTRANSIENT  XA_RBBASE+7         /* May retry the transaction branch */
#define XA_RBEND        XA_RBTRANSIENT      /* The inclusive upper bound of the rollback codes */

#define XA_NOMIGRATE    9                   /* resumption must occur where suspension occurred */
#define XA_HEURHAZ      8                   /* the transaction branch may have been heuristically completed */
#define XA_HEURCOM      7                   /* the transaction branch has been heuristically committed */
#define XA_HEURRB       6                   /* the transaction branch has been heuristically rolled back */
#define XA_HEURMIX      5                   /* the transaction branch has been heuristically committed and rolled back */
#define XA_RETRY        4                   /* routine returned with no effect and may be re-issued */
#define XA_RDONLY       3                   /* the transaction branch was read-only and has been committed */
#define XA_OK           0                   /* normal execution */
#define XAER_ASYNC      (-2)                /* asynchronous operation already outstanding */
#define XAER_RMERR      (-3)                /* a resource manager error occurred in the transaction branch */
#define XAER_NOTA       (-4)                /* the XID is not valid */
#define XAER_INVAL      (-5)                /* invalid arguments were given */
#define XAER_PROTO      (-6)                /* routine invoked in an improper context */
#define XAER_RMFAIL     (-7)                /* resource manager unavailable */
#define XAER_DUPID      (-8)                /* the XID already exists */
#define XAER_OUTSIDE    (-9)                /* resource manager doing work outside */
                                            /* global transaction */


#define TMNOFLAGS       0x00000000L         /* no resource manager features selected */
#define TMREGISTER      0x00000001L         /* resource manager dynamically registers */
#define TMNOMIGRATE     0x00000002L         /* resource manager does not support association migration */
#define TMUSEASYNC      0x00000004L         /* resource manager supports asynchronous operations */
/*
 * Flag definitions for xa_ and ax_ routines
 */
/* use TMNOFLAGS, defined above, when not specifying other flags */
#define TMASYNC         0x80000000L         /* perform routine asynchronously */
#define TMONEPHASE      0x40000000L         /* caller is using one-phase commit optimisation */
#define TMFAIL          0x20000000L         /* dissociates caller and marks transaction branch rollback-only */
#define TMNOWAIT        0x10000000L         /* return if blocking condition exists */
#define TMRESUME        0x08000000L         /* caller is resuming association with suspended transaction branch */
#define TMSUCCESS       0x04000000L         /* dissociate caller from transaction branch */
#define TMSUSPEND       0x02000000L         /* caller is suspending, not ending, association */
#define TMSTARTRSCAN    0x01000000L         /* start a recovery scan */
#define TMENDRSCAN      0x00800000L         /* end a recovery scan */
#define TMMULTIPLE      0x00400000L         /* wait for any asynchronous operation */
#define TMJOIN          0x00200000L         /* caller is joining existing transaction branch */
#define TMMIGRATE       0x00100000L         /* caller intends to perform migration */


typedef struct xid_t XID;
typedef struct xid_s XID_SHORT;


enum class XaOperation { start, end, prepare, commit, rollback, forget, recover, getTimeout, setTimeout, prepareEx, rollbackEx, forgetEx };
const int OP_START      =  0;
const int OP_END        =  1;
const int OP_PREPARE    =  2;
const int OP_COMMIT     =  3;
const int OP_ROLLBACK   =  4;
const int OP_FORGET     =  5;
const int OP_RECOVER    =  6;
const int OP_GETTIMEOUT =  7;
const int OP_SETTIMEOUT =  8;

// extended operations, not called directly by client
const int OP_PREPAREEX  =  9;
const int OP_ROLLBACKEX =  10;
const int OP_FORGETEX   =  11;


typedef struct XACallParam {
    unsigned int sizeParam;
    int          operation;
    XID          xid;
    int          flags;
    int          status;
    unsigned int sizeData;
    unsigned int sizeReturned;
} XACALLPARAM, *PXACALLPARAM; 

#define FLAG_TIGHTLYCOUPLED  0x8000

```
