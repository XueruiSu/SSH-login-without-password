使用公钥免密登录。基本逻辑：在本地生成公钥和私钥，在公钥的路径下执行相应的命令将公钥传到服务器上。每次连服务器的时候本机和服务器会自动匹配公钥和私钥，若匹配成功则自动连接。如此便可达到免密登录的目的。

1.使用ssh-keygen 生成密钥 若要创建密钥，首选命令是：ssh-keygen（输入这个命令然后按照要求一直点回车就行）

2.在本机的powershell里cd到C:\Users\user_name\.ssh目录下，执行以下命令：
	ssh-copy-id -i id_rsa.pub xuerui@211.71.74.225

注：
ssh-copy-id在powershell里面第一次用会报错“找不到此命令”。所以要先加载这个命令：
在power shell里运行下面的程序：
function ssh-copy-id([string]$userAtMachine, $args){   
    $publicKey = "$ENV:USERPROFILE" + "/.ssh/id_rsa.pub"
    if (!(Test-Path "$publicKey")){
        Write-Error "ERROR: failed to open ID file '$publicKey': No such file"            
    }
    else {
        & cat "$publicKey" | ssh $args $userAtMachine "umask 077; test -d .ssh || mkdir .ssh ; cat >> .ssh/authorized_keys || exit 1"      
    }
}
