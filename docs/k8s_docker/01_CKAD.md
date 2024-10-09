---
sidebar_position: 1
---

# CKAD - Commands 

- Show Labels   
  `k get po --show-label`
---
- Delete pod with label    
  `k delete po -l app=webapp`
---
- Delete pod without wait   
  `k delete po my-app --grace-period=0 --force`
---
- Generate template with command   
  `k run my-app --image ubuntu --dry-run=client -o yaml --command -- sleep 10`
---
- Generate template with args   
  `k run my-app --image ubuntu --dry-run=client -o yaml -- sh`
---
- Get all api resources   
  `k api-resources`
---
- Create pod with env variable   
  `k run my-app --image ubuntu --env MY_KEY=foo`
---
- Explain resource and find it    
  `k explain pod --recursive | grep -C5 -i env`
---
- Set serviceaccount to deployement    
  `k set sa deployment my-app my-sa`
---
- Get CPU / Memory    
  `k top pod`
  `k top node`
---
- Get resource by label     
  `k get po --selector env=dev`     
  `k get all --selector env=prod,bu=finance,tier=frontend`
---
- Set context     
  `k config --kubeconfig=/root/my-kube-config current-context my-context`
---
- Run command as a different use  
  `k get pods --as dev-user`
---
- Get list of default admission-plugins   
  `kubectl exec -it -n kube-system kube-apiserver-controlplane -- kube-apiserver -h | grep -i enable-admission-plugins`
---
- Enable api verison alphav1   
  add `--runtime-config=rbac.authorization.k8s.io/v1alpha1` in `/etc/kubernetes/manifests/kube-apiserver.yaml`  
- Convert api version using kubectl version   
  `kubectl-convert -f ingress-old.yaml -- output-version networking.k8s.io/v1 `  


kubectl-convert -f ingress-old.yaml -- output-version networking.k8s.io/v1
### Vim Shortcuts

- Starting of line   
  `0`
---
- End of line   
  `$`
---
- Undo       
  `u`
---
- Redo       
  `ctrl + r`
---
- Append       
  `a`
---
- Multi line edit (add in front)   
  `control + v` --> select lines --> `shift + i` --> add your changes --> `esc`
---
- Multi line edit (delete in front)  
  `control + v` --> select lines --> select area --> `d` --> add your changes --> `esc`
---

