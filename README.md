# NFA-DFAfirst_step
http://blog.csdn.net/u011520133/article/details/50333981 
leetCode65Validnumber
输入一个字符串判断是不是合法数字
以下情况 state 0 ' ' 1 z 2 . 3 z.z 4 Se 5 Sez 6 z. 7 Se+/Se-
1."46.e3" true
2." " false
3."." false
4.".2" true
AC的我猝不及防
class Solution {
public:
    bool isNumber(string s) {
        int flag = 0;//state 0 ' ' 1 z 2 . 3 z.z 4 Se 5 Sez 6 z. 7 Se+/Se-
        string::iterator it = s.begin();
        while(*it==' ')it++;
        if(it==s.end()) return false;
        if(*it=='-'||*it=='+')it++;
        int state = 0;
        for( ;it < s.end()&&*it!=' ';it++){
              if(*it <= '9'&&*it >= '0'  ){
                  
                  if(state == 0) state = 1;
                  if(state == 2||state==6) state = 3;
                  if(state == 4||state==7) state = 5;
                   
              }
         else{
              if(*it=='.'){
                  if(state == 0) state=2;
                  else if(state == 1) state = 6;
                  else return false;
                  continue;
              }
              if(*it=='e'){
                if(state==1||state==3||state==6)  state=4;
                else  return false;
                  continue;
              }
             if(*it=='+'||*it=='-') {
                 if(state==4||state==0) state=7;
                 else return false;
                 continue;
             }
                 return false;
              }
             
        }
         
        if(state==2||state==4||state==7) return false;
        while(it < s.end()&&*it==' ')it++;
        if( it!=s.end() ) return false;
        return true;
    }
};
