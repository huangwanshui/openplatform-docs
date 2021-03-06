## 获取设备列表

<style>
	table{
		border-collapse:collapse;
		width:100%;
	}
	table tr td{
		border:1px solid #000;
	}
</style>
<table >
<tr><td style="background-color:#ccc;text-align:center;width:100px;">定义</td><td colspan="2">int FUN_SysGetDevList(UI_HANDLE hUser, const char *szUser, const char *szPwd, int nSeq = 0);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">获取设备列表</td></tr>
<tr><td rowspan="5" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明
</td></tr>
<tr><td style="text-align:center">hUser
</td><td>结果接收者<label style="color:red">（其它方法此参数的意义相同）</label></td></tr>
<tr><td style="text-align:center">szUser
</td><td>用户名（本地登录方式暂时验证）</td></tr>
<tr><td style="text-align:center">password</td><td>密码（本地登录方式暂时验证）</td></tr>
<tr><td style="text-align:center">nSeq
</td><td>消息回调的seq值<label style="color:red">（其它方法此参数的意义相同）</label>
</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id</td>
<td>消息值：EUIMSG.EMSG_SYS_GET_DEV_INFO_BY_USER
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>>=0：设备条数；<0：失败，详见错误码说明</td></tr>
<tr><td style="text-align:center">pData
</td><td>指向SDBDeviceInfo数组的字节流（可使用G.BytesToObj转换字节流与对象之间的）</td></tr>
</table>

## 获取设备列表(第三方获取)

<table >
<tr><td style="background-color:#ccc;text-align:center;width:100px;">定义</td><td colspan="2">int FUN_SysGetDevListEx(UI_HANDLE hUser, const char *unionId, const char *szType, int nApptype, int nSeq = 0);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">第三方获取列表接口（微信、QQ、微博等）</td></tr>
<tr><td rowspan="5" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明
</td></tr>
<tr><td style="text-align:center">unionId
</td><td>唯一ID</td></tr>
<tr><td style="text-align:center">szType
</td><td>第三方类型(例:微信“wx”)</td></tr>
<tr><td style="text-align:center">password</td><td>密码（本地登录方式暂时验证）</td></tr>
<tr><td style="text-align:center">nApptype
</td><td>app类型
</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id</td>
<td>消息值：EUIMSG.EMSG_SYS_GET_DEV_INFO_BY_USER
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>>=0：设备条数；<0：失败，详见错误码说明</td></tr>
<tr><td style="text-align:center">pData
</td><td>指向SDBDeviceInfo数组的字节流（可使用G.BytesToObj转换字节流与对象之间的）</td></tr>
</table>
unionId	
	
	

## 添加设备

<table >
<tr><td style="background-color:#ccc;text-align:center;width:100px;">定义</td><td colspan="2">int FUN_SysAdd_Device(UI_HANDLE hUser, SDBDeviceInfo *pDevInfo, const char *szExInfo = "", const char *szExInfo2 = "", int nSeq = 0);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">添加设备</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明
</td></tr>
<tr><td style="text-align:center">pDevInfo</td>
<td>
设备信息对象字节流<br><pre>
typedef struct SDBDeviceInfo
{
   &nbsp char Devmac[64]; //DEV_SN/IP/DNS
   &nbsp char Devname[128]; //名称
   &nbsp char devIP[64]; //设备ip
   &nbsp char loginName[16]; //用户名
   &nbsp char loginPsw[16]; //密码
   &nbsp int nPort; //端口映射端口
   &nbsp int nType; //--设备类型 1:插座
   &nbsp int nID; //--本设备ID,内部使用
}SDBDeviceInfo;</pre>
</td></tr>
<tr><td  style="text-align:center">szExInfo
</td><td>系统用户名；为空时表示与调用SysGetDevList使用的用户名相同<br>格式:param1=value1&param2=value2<br>
其中“ma=true&delOth=true”设置此帐户为此设备的主帐户<br>
其中“ext=XXXXXXXX”设置设备的用户自定义信息</td></tr>
<tr><td  style="text-align:center">szExInfo2</td><td>暂时未使用</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td  style="text-align:center">id
</td><td>消息值：EUIMSG . EMSG_SYS_ADD_DEVICE</td></tr>
<tr><td  style="text-align:center">arg1</td>
<td>==0：成功；<0：失败，详见错误码说明</td></tr>
</table>

## 通过文件添加设备

<table >
<tr><td style="background-color:#ccc;text-align:center;width:50px;">定义</td><td colspan="2">int Fun_SysAddDevByFile(UI_HANDLE hUser, const char *szPath, int nSeq = 0);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">通过文件添加设备</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明
</td></tr>
<tr><td style="text-align:center">szPath</td>
<td>设备信息文件（含路径）</td></tr>

<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td  style="text-align:center">id
</td><td>消息值：EUIMSG  . EMSG_SYS_ADD_DEVICE_BY_FILE
</td></tr>
<tr><td  style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td></tr>
</table>

## 删除设备

<table >
<tr><td style="background-color:#ccc;text-align:center;width:50px;">定义</td><td colspan="2">int FUN_SysDelete_Dev(UI_HANDLE hUser, const char *Delete_DevMac,const char *UserName,const char *Psw, int nSeq = 0);   </td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">删除设备</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明
</td></tr>
<tr><td style="text-align:center">Delete_DevMac</td>
<td>设备序列号</td></tr>
<tr><td style="text-align:center">userName
</td><td>系统用户名；为空时表示与调用SysGetDevList使用的用户名相同</td></tr>
<tr><td  style="text-align:center">Psw</td><td>系统密码；为空时表示与调用SysGetDevList使用密码相同</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td  style="text-align:center">id
</td><td>消息值：EUIMSG  . EMSG_SYS_DELETE_DEV
</td></tr>
<tr><td  style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td></tr>
</table>

## 修改设备

<table >
<tr><td style="background-color:#ccc;text-align:center;width:35px;">定义</td><td colspan="2">int FUN_SysChangeDevInfo(UI_HANDLE hUser, struct SDBDeviceInfo *ChangeDevInfor,const char *UserName,const char *Psw, int nSeq = 0); 
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">修改设备</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明
</td></tr>
<tr><td style="text-align:center">ChangeDevInfor
</td>
<td>设备信息：SDBDeviceInfo 参考上面下定义
</td></tr>
<tr><td style="text-align:center">userName
</td><td>系统用户名；为空时表示与调用SysGetDevList使用的用户名相同</td></tr>
<tr><td  style="text-align:center">Psw</td><td>系统密码；为空时表示与调用SysGetDevList使用密码相同</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG.   EMSG_SYS_CHANGEDEVINFO
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td></tr>
</table>

## 加密设备序列号

<table >
<tr><td style="background-color:#ccc;text-align:center;width:35px;">定义</td><td colspan="2">char *FUN_EncDevInfo(char *szDevInfo, const char *szDevId, const char *szUser, const char *szPwd, int nType);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">加密设备序列号</td></tr>
<tr><td rowspan="5" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明
</td></tr>
<tr><td style="text-align:center">szDevId</td><td>设备序列号</td></tr>
<tr><td style="text-align:center">szUser
</td><td>系统用户名；为空时表示与调用SysGetDevList使用的用户名相同</td></tr>
<tr><td  style="text-align:center">Psw</td><td>系统密码；为空时表示与调用SysGetDevList使用密码相同</td></tr>
<tr><td style="text-align:center">nType</td>
<td>类型
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">返回</td><td colspan="2" style="text-align:center";>加密过后的设备序列号
</td><tr>
</table>

## 解密设备序列号

<table >
<tr><td style="background-color:#ccc;text-align:center;width:35px;">定义</td><td colspan="2">char *FUN_DecDevInfo(const char *szDevInfo, char *szResult)
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">解密设备序列号</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明
</td></tr>
<tr><td style="text-align:center">szDevInfo</td><td>需要解密的设备信息</td></tr>

<tr><td style="background-color:#ccc;text-align:center">返回</td><td colspan="2" style="text-align:center";>解密过后的设备序列号
</td><tr>
</table>

## 修改密码

<table >
<tr><td style="background-color:#ccc;text-align:center;width:35px;">定义</td><td colspan="2">int FUN_SysPsw_Change(UI_HANDLE hUser, const char *UserName,const char *old_Psw,const char *new_Psw, int nSeq = 0);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">修改密码</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明
</td></tr>
<tr><td style="text-align:center">userName</td>
<td>用户名</td></tr>
<tr><td style="text-align:center">old_Psw</td>
<td>老密码</td></tr>
<tr><td style="text-align:center">new_Psw</td>
<td>新密码</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td  style="text-align:center">id
</td><td>消息值：EUIMSG . EMSG_SYS_PSW_CHANGE
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>> ==0：成功；<0：失败，详见错误码说明</td></tr>
</table>

## 恢复密码

<table >
<tr><td style="background-color:#ccc;text-align:center;width:35px;">定义</td><td colspan="2">int SysPswRestore(int hUser, String UserName,String new_Psw, int nSeq);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">用户密码恢复</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明
</td></tr>
<tr><td style="text-align:center">UserName</td>
<td>用户名</td></tr>
<tr><td style="text-align:center">new_Psw</td>
<td>密码</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td  style="text-align:center">id
</td><td>消息值：EUIMSG . EMSG_SYS_PSW_RESTORE
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>> ==0：成功；<0：失败，详见错误码说明</td></tr>
</table>

## 通过邮箱找密码

<table >
<tr><td style="background-color:#ccc;text-align:center;width:35px;">定义</td><td colspan="2">int Fun_SysGetPWByEmail(UI_HANDLE hUser, const char* UserName, int nSeq = 0);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">找回密码，会向注册邮箱里发送修改密码的链接。</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明
</td></tr>
<tr><td style="text-align:center">UserName</td>
<td>用户名</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td  style="text-align:center">id
</td><td>消息值：EUIMSG . EMSG_SYS_GETPWBYEMAIL
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>> ==0：成功；<0：失败，详见错误码说明</td></tr>
</table>

## 获取设备状态

<table >
<tr><td style="background-color:#ccc;text-align:center;width:35px;">定义</td><td colspan="2">int FUN_SysGetDevState(UI_HANDLE hUser, const char *devId, int nSeq = 0);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">获取设备状态，可多个一起查询，以；分割</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明
</td></tr>
<tr><td style="text-align:center">devIds</td>
<td>设备序列号</td></tr>

<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td  style="text-align:center">id
</td><td>消息值：EUIMSG   . EMSG_SYS_GET_DEV_STATE
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>> 0：在线</td></tr>
<tr><td style="text-align:center">str
</td><td>单个设备序列号</td></tr>
<tr><td>备注</td><td colspan="2">若多个设备一起查询，设备状态会分开返回</td></tr>
</table>

## 分类型获取设备状态
<table >
<tr><td style="background-color:#ccc;text-align:center;width:35px;">定义</td><td colspan="2">int FUN_GetDevState(const char *szDevId, int nType);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">分类型获取设备状态（直接获取缓存中的状态）</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明
</td></tr>
<tr><td style="text-align:center">nType</td>
<td>设备类型，详见枚举EFunDevStateType</td></tr>
<tr><td style="background-color:#ccc;text-align:center">返回</td><td colspan="2" style="text-align:center";>返回值见枚举EFunDevState
</td><tr>
</table>

## 用户账号绑定

<table >
<tr><td style="background-color:#ccc;text-align:center;width:35px;">定义</td><td colspan="2">int FUN_SysBindingAccount(UI_HANDLE hUser, const char *name, const char *pwd, int nSeq = 0);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">name，pwd不为空时，绑定现有的帐户和密码<br>
name，pwd为空时，自动生成一个用户名和密码
</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明
</td></tr>
<tr><td style="text-align:center">name</td>
<td>用户名</td></tr>
<tr><td style="text-align:center">pwd</td>
<td>密码</td></tr>

<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td  style="text-align:center">id
</td><td>消息值：EUIMSG . EMSG_SYS_BINDING_ACCOUNT
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td></tr>
<tr><td style="text-align:center">str
</td><td>绑定的用户名和密码组成的字符串</td></tr>
</table>

## 获取手机验证码

<table >
<tr><td style="background-color:#ccc;text-align:center;width:35px;">定义</td><td colspan="2">int FUN_SysSendPhoneMsg(UI_HANDLE hUser, const char *UserName, const char *phoneNO, int nSeq = 0);  
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">获取手机验证码(用户注册)</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明
</td></tr>
<tr><td  style="text-align:center">userName</td>
<td>用户名</td></tr>
<tr><td style="text-align:center">phoneNO</td>
<td>手机号码</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG  . EMSG_SYS_GET_PHONE_CHECK_CODE</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td></tr>
</table>

## 用户注册（手机号）

<table >
<tr><td style="background-color:#ccc;text-align:center;width:35px;">定义</td><td colspan="2">int FUN_SysRegUserToXM(UI_HANDLE hUser, const char *UserName, const char *pwd, const char *checkCode,const char *phoneNO, int nSeq);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">用户注册(手机号)// 通用注册接口</td></tr>
<tr><td rowspan="5" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">userName
</td><td>用户名。用户名要求长度4~15位，可用中文、英文、数字和“_”组成 </td></tr>
<tr><td style="text-align:center">pwd</td>
<td>密码</td></tr>
<tr><td style="text-align:center">checkCode
</td><td>验证码</td></tr>
<tr><td style="text-align:center">phoneNO</td>
<td>手机号码</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id</td>
<td>消息值：EUIMSG  . EMSG_SYS_REGISER_USER_XM
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td></tr>
</table>

## 用户注册（手机号-扩展参数）

<table >
<tr><td style="background-color:#ccc;text-align:center;width:35px;">定义</td><td colspan="2">iint FUN_SysRegUserToXMExtend(UI_HANDLE hUser, const char *UserName, const char *pwd, const char *checkCode, const char *phoneNO, const char *source, const char *country, const char *city, int nSeq = 0);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">用户注册(手机号-扩展参数)</td></tr>
<tr><td rowspan="8" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">userName
</td><td>用户名。用户名要求长度4~15位，可用中文、英文、数字和“_”组成 </td></tr>
<tr><td style="text-align:center">pwd</td>
<td>密码</td></tr>
<tr><td style="text-align:center">checkCode
</td><td>验证码</td></tr>
<tr><td style="text-align:center">phoneNO</td>
<td>手机号码</td></tr>
<tr><td style="text-align:center">source</td>
<td>注册来源</td></tr>
<tr><td style="text-align:center">country</td>
<td>国家</td></tr>
<tr><td style="text-align:center">city</td>
<td>城市</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id</td>
<td>消息值：EUIMSG  . EMSG_SYS_REGISER_USER_XM_EXTEND
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td></tr>
</table>

## 修改用户密码

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysEditPwdXM(UI_HANDLE hUser, const char *UserName, const char *oldPwd, const char *newPwd, int nSeq);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">修改用户密码
</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">userName
</td><td>用户名</td></tr>
<tr><td style="text-align:center">oldPwd</td>
<td>旧密码</td></tr>
<tr><td style="text-align:center">newPwd
</td><td>新密码</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG  . EMSG_SYS_EDIT_PWD_XM
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td></tr>
</table>

## 忘记登录密码

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysForgetPwdXM(UI_HANDLE hUser, const char *phoneOrEmail, int nSeq);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">忘记登录密码(获取验证码)
</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">phoneOrEmail</td>
<td>手机号码</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG   . EMSG_SYS_FORGET_PWD_XM
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td></tr>
</table>

## 验证验证码（手机或邮箱）

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_CheckResetCodeXM(UI_HANDLE hUser, const char *phoneOrEmail, const char *checkNum, int nSeq);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">验证修改密码的验证码是否正确</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">phoneOrEmail</td>
<td>手机号码或者邮箱</td></tr>
<tr><td style="text-align:center">checkNum</td>
<td>验证码</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG  . EMSG_SYS_REST_PWD_CHECK_XM</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td></tr>
</table>

## 重置登录密码

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_ResetPwdXM(UI_HANDLE hUser, const char *phoneOrEmail, const char *newPwd, int nSeq);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">验证修改密码的验证码是否正确</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">phone</td>
<td>手机号码或者邮箱</td></tr>
<tr><td style="text-align:center">newPwd</td>
<td>新密码</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG  . EMSG_SYS_RESET_PWD_XM
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td></tr>
</table>

## 同步登录

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysLoginToXM(UI_HANDLE hUser, const char *UserName, const char *pwd, int nSeq);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">同步登录
</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">UserName
</td><td>用户名</td></tr>
<tr><td style="text-align:center">pwd</td>
<td>密码</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG   . EMSG_ SYS_GET_DEV_INFO_BY_USER_XM
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td></tr>
</table>

## 同步退出

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysLogout(UI_HANDLE hUser, int nSeq = 0);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">同步退出
</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr style="text-align:center"><td>无
</td><td>   </td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG   . EMSG_SYS_LOGOUT_TO_XM
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td></tr>
</table>

## 视频广场登陆

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_XMVideoLogin(UI_HANDLE hUser, const char *szUser, const char *szPwd, int nSeq);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">视频广场登陆
</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">UserName
</td><td>用户名</td></tr>
<tr><td style="text-align:center">passWord</td>
<td>密码</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG . XM030_VIDEO_LOGIN
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td></tr>
</table>

## 视频广场退出

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_XMVideoLogout(UI_HANDLE hUser, int nSeq);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">视频广场退出
</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr style="text-align:center"><td>无
</td><td>   </td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：消息值：EUIMSG . XM030_VIDEO_LOGOUT
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td></tr>
</table>

## 上传本地视频文件

<table >
<tr><td style="background-color:#ccc;text-align:center;width:20px;">定义</td><td colspan="2">int UpLoadLocalVideo(int hUser, String title, String location, String description, String catagroyId, String videoFileName, String pictureFileName, int nSeq);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">上传本地视频文件、标题、描述、地址、类别
</td></tr>
<tr><td rowspan="7" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">title</td>
<td>标题</td></tr>
<tr><td style="text-align:center">location</td>
<td>地址</td></tr>
<tr><td style="text-align:center">description
</td><td>描述</td></tr>
<tr><td style="text-align:center">catagroyId
</td><td>分类id</td></tr>
<tr><td style="text-align:center">videoFileName
</td><td>视频本地路径</td></tr>
<tr><td style="text-align:center">pictureFileName
</td><td>视频缩略图本地路径</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG   . EMSG_SYS_DEV_UPLOAD_VIDEO
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；>   0 是进度 <0：失败，详见错误码说明</td></tr>
</table>

## 删除目录下文件

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int GN_DeleteFiles(const char *szDir, long nDaysAgo, const char *szType);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">删除指定目录上，指定日期之前，指定后缀名的文件</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">szDir</td>
<td>目录</td></tr>
<tr><td style="text-align:center">nDaysAgo</td>
<td>日期</td></tr>
<tr><td style="text-align:center">szType
</td><td>后缀名</td></tr>
<tr><td style="background-color:#ccc;text-align:center">返回</td><td colspan="2" style="text-align:center";>>=0 返回删除文件数  <0删除失败
</td><tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：无</td></tr>
<tr><td style="text-align:center">arg1
</td><td></td></tr>
</table>

## 检查产品真伪

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysCheckDeviceReal(UI_HANDLE hUser, const char *twoDimensionCode, int nSeq = 0);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
 检查产品真伪</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">twoDimensionCode</td>
<td>设备二维码</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG   . EMSG_SYS_CHECK_DEVIDE_REAL 5040
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
<tr><td style="text-align:center">str
</td><td>获取到的josn数据</td>
</tr>
</table>

## 检查密码合法性和强度

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_CheckPwdStrength(UI_HANDLE hUser, const char *newPwd, int nSeq);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
 检查密码合法性和强度</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">pwd</td>
<td>密码</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG . EMSG_SYS_CHECK_PWD_STRENGTH
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
<tr><td style="text-align:center">str
</td><td>获取到的josn数据</td>
</tr>
</table>

## 获取邮箱验证码

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysSendEmailCode(UI_HANDLE hUser, const char *email, int nSeq);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
 获取邮箱验证码(用户注册)</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">email</td>
<td>邮箱账号</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>
 消息值：EUIMSG   . EMSG_SYS_SEND_EMAIL_CODE</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
<tr><td style="text-align:center">str
</td><td>获取到的josn数据</td>
</tr>
</table>

## 获取邮箱验证码-扩展

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysSendEmailCodeEx(UI_HANDLE hUser, const char *email, const char *username, int nSeq);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
 获取邮箱验证码(用户注册-扩展)</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">email</td>
<td>邮箱账号</td></tr>
<tr><td style="text-align:center">username</td>
<td>用户名</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>
 消息值：EUIMSG . EMSG_SYS_SEND_EMAIL_CODE</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
<tr><td style="text-align:center">str
</td><td>获取到的josn数据</td>
</tr>
</table>

## 用户注册（邮箱）

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysRegisteByEmail(UI_HANDLE hUser, const char *userName, const char *password, const char *email, const char *code, int nSeq);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
 用户注册（邮箱）</td></tr>
<tr><td rowspan="5" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">userName</td>
<td>用户名。用户名要求长度4~15位，可用中文、英文、数字和“_”组成 </td></tr>
<tr><td style="text-align:center">password</td>
<td>密码</td></tr>
<tr><td style="text-align:center">email</td>
<td>邮箱</td></tr>
<tr><td style="text-align:center">code</td>
<td>验证码</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG   . EMSG_SYS_REGISTE_BY_EMAIL
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
<tr><td style="text-align:center">str
</td><td>获取到的josn数据</td>
</tr>
</table>

## 用户注册（邮箱-扩展）

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysRegisteByEmailExtend(UI_HANDLE hUser, const char *userName, const char *password, const char *email, const char *code, const char *source, const char *country, const char *city, int nSeq = 0);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
 用户注册（邮箱-扩展）</td></tr>
<tr><td rowspan="8" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">userName</td>
<td>用户名。用户名要求长度4~15位，可用中文、英文、数字和“_”组成 </td></tr>
<tr><td style="text-align:center">password</td>
<td>密码</td></tr>
<tr><td style="text-align:center">email</td>
<td>邮箱</td></tr>
<tr><td style="text-align:center">code</td>
<td>验证码</td></tr>
<tr><td style="text-align:center">source</td>
<td>注册来源</td></tr>
<tr><td style="text-align:center">country</td>
<td>国家</td></tr>
<tr><td style="text-align:center">city</td>
<td>城市</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG . EMSG_SYS_REGISTE_BY_EMAIL_EXTEND
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
<tr><td style="text-align:center">str
</td><td>获取到的josn数据</td>
</tr>
</table>

## 找回密码 （重置）- 发送邮箱验证码

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysSendCodeForEmail(UI_HANDLE hUser, const char *email, int nSeq);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
 获取邮箱验证码（修改密码）</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">email</td>
<td>邮箱账号</td></tr>

<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG   . EMSG_SYS_SEND_EMAIL_FOR_CODE</td></tr>
<tr><td style="text-align:center">arg1</td>
<td>==0：成功；<0：失败，详见错误码说明</td></tr>
<tr><td style="text-align:center">str
</td><td>获取到的josn数据</td>
</tr>
</table>

## 找回密码 （重置）-扩展 发送邮箱验证码

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysSendCodeForEmailEx(UI_HANDLE hUser, const char *email, const char *username, int nSeq);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
 获取邮箱验证码（修改密码）</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">email</td>
<td>邮箱账号</td></tr>
<tr><td style="text-align:center">username</td>
<td>用户名</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG   . EMSG_SYS_SEND_EMAIL_FOR_CODE</td></tr>
<tr><td style="text-align:center">arg1</td>
<td>==0：成功；<0：失败，详见错误码说明</td></tr>
<tr><td style="text-align:center">str
</td><td>获取到的josn数据</td>
</tr>
</table>

## 找回密码 （重置） – 验证邮箱验证码

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysCheckCodeForEmail(UI_HANDLE hUser, const char *email, const char *code, int nSeq);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
 验证找回密码的验证码是否正确</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">email</td>
<td>邮箱</td></tr>
<tr><td style="text-align:center">code</td>
<td>邮箱验证码</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG   . EMSG_SYS_CHECK_CODE_FOR_EMAIL</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
<tr><td style="text-align:center">str
</td><td>获取到的josn数据</td>
</tr>
</table>

## 邮箱找回密码 （重置）

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysChangePwdByEmail(UI_HANDLE hUser, const char *email, const char *newpwd, int nSeq);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
 找回密码（邮箱）</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">email</td>
<td>邮箱</td></tr>
<tr><td style="text-align:center">newpwd</td>
<td>新密码</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG   . EMSG_SYS_PSW_CHANGE_BY_EMAIL</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
</table>

## 检查用户是否已被注册

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysCheckUserRegiste(UI_HANDLE hUser, const char *userName, int nSeq =0);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
检查用户是否已被注册</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">userName</td>
<td>用户名</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG   . EMSG_SYS_CHECK_USER_REGISTE</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
<tr><td style="text-align:center">str
</td><td>获取到的josn数据</td>
</tr>
</table>

## 检查用户手机号是否已被注册

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">FUN_HANDLE FUN_CheckUserPhone(UI_HANDLE hUser, const char *phone, int nSeq);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
检查用户手机号是否已被注册</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">phone</td>
<td>手机号码</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG   . EMSG_SYS_CHECK_USER_PHONE</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
<tr><td style="text-align:center">str
</td><td>获取到的josn数据</td>
</tr>
</table>

## 检查用户邮箱是否已被注册

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">FUN_HANDLE FUN_CheckUserMail(UI_HANDLE hUser, const char *mail, int nSeq);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
检查用户邮箱是否已被注册</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">mail</td>
<td>邮箱</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG   . EMSG_SYS_CHECK_USER_MAIL</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
<tr><td style="text-align:center">str
</td><td>获取到的josn数据</td>
</tr>
</table>

## 获取用户信息

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysGetUerInfo(UI_HANDLE hUser, const char *userName, const char *pwd, int nSeq = 0);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
获取用户信息</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">userName</td>
<td>用户名</td></tr>
<tr><td style="text-align:center">pwd</td>
<td>密码</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG  . EMSG_SYS_GET_USER_INFO
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
<tr><td style="text-align:center">str
</td><td>获取到的josn数据</td>
</tr>
</table>

## 绑定安全手机(1)—发送验证码 

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysSendBindingPhoneCode(UI_HANDLE hUser, const char *phone, const char *userName, const char *pwd, int nSeq  =0);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
发送验证码到手机 </td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">phone</td>
<td>手机号码</td></tr>
<tr><td style="text-align:center">userName</td>
<td>用户名</td></tr>
<tr><td style="text-align:center">pwd</td>
<td>密码</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG  . EMSG_SYS_SEND_BINDING_PHONE_CODE
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
<tr><td style="text-align:center">str
</td><td>获取到的josn数据</td>
</tr>
</table>

## 绑定安全手机(2)—验证code并绑定 

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysBindingPhone(UI_HANDLE hUser, const char *userName, const char *pwd, const char *phone, const char *code, int nSeq  =0);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
绑定手机号 </td></tr>
<tr><td rowspan="5" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">userName</td>
<td>用户名</td></tr>
<tr><td style="text-align:center">pwd</td>
<td>密码</td></tr>
<tr><td style="text-align:center">phone</td>
<td>手机号</td></tr>
<tr><td style="text-align:center">code</td>
<td>验证码</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG  . EMSG_SYS_BINDING_PHONE
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
<tr><td style="text-align:center">str
</td><td>获取到的josn数据</td>
</tr>
</table>

## 绑定安全邮箱(1)—发送验证码 

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysSendBindingEmailCode(UI_HANDLE hUser, const char *email, const char *userName, const char *pwd, int nSeq);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
发送验证码到邮箱 </td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">email</td>
<td>邮箱账户</td></tr>
<tr><td style="text-align:center">userName</td>
<td>用户名</td></tr>
<tr><td style="text-align:center">pwd</td>
<td>密码</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG  . EMSG_SYS_SEND_BINDING_EMAIL_CODE
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
<tr><td style="text-align:center">str
</td><td>获取到的josn数据</td>
</tr>
</table>

## 绑定安全邮箱(2)—验证code并绑定 

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysBindingEmail(UI_HANDLE hUser, const char *userName, const char *pwd, const char *email, const char *code, int nSeq);</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
绑定邮箱 </td></tr>
<tr><td rowspan="5" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">userName</td>
<td>用户名</td></tr>
<tr><td style="text-align:center">pwd</td>
<td>密码</td></tr>
<tr><td style="text-align:center">email</td>
<td>邮箱账户</td></tr>
<tr><td style="text-align:center">code</td>
<td>验证码</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG  . EMSG_SYS_BINDING_EMAIL
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
<tr><td style="text-align:center">str
</td><td>获取到的josn数据</td>
</tr>
</table>

## 检查APP更新

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int Fun_FirLatest(UI_HANDLE hUser, const char *appId, const char *appToken, int nSeq = 0);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
检查APP更新</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">appToken</td>
<td>包名</td></tr>
<tr><td style="text-align:center">appId</td>
<td>App Id</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG   . EMSG_FIR_IM_CHECK_LATEST
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
<tr><td style="text-align:center">str
</td><td>获取到的josn数据</td>
</tr>
</table>

## 开启上报数据

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int DevStartUploadData(int hUser, String szDevId,int nUploadDataType, int nSeq);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
开启上报数据</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr style="text-align:center"><td>szDevId</td>
<td>设备序列号</td></tr>
<tr><td style="text-align:center">nUploadDataType
</td>
<td>上报数据类型：<br>
VEHICLE =   0;// 车载信息<br>
SDK_RECORD_STATE   = 1;// 录像状态<br>
SDK_DIGITCHN_STATE   = 2; // 数字通道连接状态<br>
SDK_TITLE_INFO   = 3; // 通道标题<br>
SDK_FUNCTION_STATE   = 4;// 功能状态   如：运动相机
// 录像状态、延时拍状态等<br>
SDK_ELECT_STATE   = 5;// 电量状态
</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id</td>
<td>消息值：EUIMSG   . EMSG_DEV_START_UPLOAD_DATA<br>
DEV_ON_UPLOAD_DATA   回调中返回 上报数据、进度、数据类型
</td></tr>
<tr ><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td></tr>
</table>

## 关闭上报数据

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int DevStopUploadData(int hUser, String szDevId,int nUploadDataType, int nSeq);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
关闭上报数据</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">szDevId</td>
<td>设备序列号</td></tr>
<tr><td style="text-align:center">nUploadDataType</td>
<td>上报数据类型：类型说明同上</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG   . EMSG_FIR_IM_CHECK_LATEST
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
</table>

## 返回设备是否开启了微信报警推送

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysDevWXPMS(const char *szDeviceSN);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
返回设备是否开启了微信报警推送</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">szDeviceSN</td>
<td>设备序列号</td></tr>
<tr><td style="background-color:#ccc;text-align:center">返回</td><td colspan="2" style="text-align:center";>返回是否开启int；>=0开启
</td><tr>
</table>

## 返回设备登录帐户是否是主帐户

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysDevIsMasterAccount(const char *szDeviceSN);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
返回设备登录帐户是否是主帐户</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">szDeviceSN</td>
<td>设备序列号</td></tr>
<tr><td style="background-color:#ccc;text-align:center">返回</td><td colspan="2" style="text-align:center";>返回是否开启int；>=0开启
</td><tr>
</table>

## 获取设备的备注信息

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysGetDevComment(const char *szDeviceSN, char comment[512]);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
获取设备的备注信息</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">szDeviceSN</td>
<td>设备序列号</td></tr>
<tr><td style="background-color:#ccc;text-align:center">返回</td><td colspan="2" style="text-align:center";>返回获取到的备注信息
</td><tr>
</table>

## 开启微信报警监听

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysOpenWXAlarmListen(UI_HANDLE hUser, const char *szDeviceSN, int nSeq = 0);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
开启微信报警监听</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">sDevId</td>
<td>设备序列号</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG . EMSG_SYS_WX_ALARM_LISTEN_OPEN
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
<tr><td style="text-align:center">str
</td><td>返回的josn数据</td>
</tr>
</table>

## 关闭微信报警监听

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysCloseWXAlarmListen(UI_HANDLE hUser, const char *szDeviceSN, int nSeq = 0);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
关闭微信报警监听</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">sDevId</td>
<td>设备序列号</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG . EMSG_SYS_WX_ALARM_LISTEN_CLOSE
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
<tr><td style="text-align:center">str
</td><td>返回的josn数据</td>
</tr>
</table>

## 微信报警状态查询

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysWXAlarmStateCheck(UI_HANDLE hUser, const char *szDeviceSN, int nSeq = 0);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
微信报警状态查询</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">sDevId</td>
<td>设备序列号</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG . EMSG_SYS_WX_ALARM_WXPMSCHECK
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
<tr><td style="text-align:center">str
</td><td>返回的josn数据</td>
</tr>
</table>

## 查询云存储状态

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int Fun_SysGetDevsCSStatus(UI_HANDLE hUser, const char *szDevices, int nSeq);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
实时从服务器上查询云存储状态</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">szDevices</td>
<td>设备序列号，多个设备用","号分隔</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG . EMSG_SYS_CHECK_CS_STATUS(5067)
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
<tr><td style="text-align:center">str
</td><td>josn数据</td>
</tr>
</table>

## 获取设备所在的帐户信息

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int Fun_SysGetDevUserInfo(UI_HANDLE hUser, const char *szDevice, int nSeq);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
获取设备所在的帐户信息</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">szDevice</td>
<td>设备序列号</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG . EMSG_SYS_DULIST(5068)
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
<tr><td style="text-align:center">str
</td><td>返回的josn数据</td>
</tr>
</table>

## 指定设备的主帐户

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int Fun_SysSetDevMasterAccount(UI_HANDLE hUser, const char *szDevice,  const char *szMAUserId, int nSeq);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
指定设备的主帐户</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">szDevice</td>
<td>设备序列号</td></tr>
<tr><td style="text-align:center">szMAUserId</td>
<td>主帐户ID</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG . EMSG_SYS_MDSETMA(5069)
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
<tr><td style="text-align:center">str
</td><td>返回的josn数据</td>
</tr>
</table>

## 修改登录用户名

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int Fun_SysModifyUserName(UI_HANDLE hUser, const char *szNewUserName, int nSeq);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
修改登录用户名（只能修改微信等绑定帐户自动生成）</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">szNewUserName</td>
<td>新的用户名</td></tr>
<tr><td rowspan="3" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG. EMSG_SYS_MODIFY_USERNAME(5070)
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>==0：成功；<0：失败，详见错误码说明</td>
</tr>
</table>

## 添加设备状态到Listener

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysAddDevStateListener(UI_HANDLE hUser);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
添加设备状态到Listener</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">hUser</td>
<td>消息结果接收者</td></tr>
<tr><td style="background-color:#ccc;text-align:center">返回</td><td colspan="2" style="text-align:center";>0
</td><tr>
</table>

## 从Listener删除设备状态

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int FUN_SysRemoveDevStateListener(UI_HANDLE hUser);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
从Listener删除设备状态</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">hUser</td>
<td>消息结果接收者</td></tr>
<tr><td style="background-color:#ccc;text-align:center">返回</td><td colspan="2" style="text-align:center";>0
</td><tr>
</table>

## 从服务器端更新当前账号是否为该设备的主账号

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">int Fun_SysIsDevMasterAccountFromServer(UI_HANDLE hUser, const char *szDevice, int nSeq);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
从服务器端更新当前账号是否为该设备的主账号</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">szDevice</td>
<td>设备序列号</td></tr>
<tr><td rowspan="4" style="background-color:#ccc;text-align:center">结果消息
</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center;">说明
</td></tr>
<tr><td style="text-align:center">id
</td><td>消息值：EUIMSG. EMSG_SYS_IS_MASTERMA
</td></tr>
<tr><td style="text-align:center">arg1
</td><td>1：主账号 0：不是主账号</td>
</tr>
<tr><td style="text-align:center">str
</td><td>返回的json信息</td>
</tr>
</table>

## 前后台切换函数

<table >
<tr><td style="background-color:#ccc;text-align:center;width:40px;">定义</td><td colspan="2">void Fun_SetActive(int nActive);
</td></tr>
<tr><td style="background-color:#ccc;text-align:center">描述</td><td colspan="2">
APP前后台切换</td></tr>
<tr><td rowspan="2" style="background-color:#ccc;text-align:center">参数说明</td><td style="background-color:#ccc;text-align:center;width:20%;">名称</td><td style="background-color:#ccc;text-align:center">说明</td></tr>
<tr><td style="text-align:center">nActive</td>
<td>切换标识</td></tr>
<tr><td style="background-color:#ccc;text-align:center">返回</td><td colspan="2" style="text-align:center";>详见错误码说明
</td><tr>
</table>
