#include <bits/stdc++.h>
using namespace std;
char s[2000000];
int ans,sze,melon,i,j,lol;
char esreg[4000000];
int coco[4000000];

char* longestPalindrome(char* s) {
    for(i=0;i<sze;i++) {
        esreg[2*i]='|';
        esreg[2*i+1]=s[i];
    }
    esreg[melon-1] = '|';
    coco[0]=0;
	int c=0,r=0,max=0;
    for(i=1;i<melon;i++) {
        if(i<r&&i+coco[2*c-i]<r) {
            coco[i]=coco[2*c-i];
        }
		else {
            int j=r+1;
            while(j<melon&&2*i-j>-1&&esreg[j]==esreg[2*i-j]) {
                j++;
            }
            coco[i]=j-i-1;
            c = i;
            r = j - 1;
            if(coco[i]>coco[max]) {
                max = i;
            }
        }
    }

    ans = coco[max];
    lol = (max - ans) / 2;
    char *bruh = (char *) malloc(sizeof(char) * (ans + 1));
    for(i = 0; i < ans; i++) {
        bruh[i] = s[i + lol];
    }
    bruh[ans] = '\0';
    return bruh;
}
int main(){
	scanf("%s",&s);
	sze=strlen(s);
	melon=sze*2+1;
	cout << longestPalindrome(s);
	cout << ans;
    return 0;
}
