    
    1. 下载对应平台的 zip 包 [https://github.com/openshift/origin/releases/]
    2. 将其中的oc用root权限放置到bin目录下
    3. 在cmd中输出oc检测


    1. oc completion bash > openshift.sh
    2. cat openshift.sh
    3. sudo mv openshift.sh /etc/bash_completion.d/
    4. source /etc/bash_completion
    5. oc logout
    6. oc login