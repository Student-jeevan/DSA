Q .. 
 Given two numbers N,X and an array A of N numbers.
 Determine if there is a way to put '+' or '-' signs between every two numbers in the array A
 in order to make an expression that is equal to X.
 Note: Solve this problem using recursion.

 Input
 First line contains two numbers N and X (1≤N≤20,−109≤X≤109) .
 Second line contains N
 distinct numbers A1,A2,....AN
 (1≤Ai≤105).
Output
Print "YES" if you can put '+' or '-' signs between every two number to create an expression that is equal to X
otherwise, print "NO".
example : 
5(n) 5(x)
v = [1 2 3 4 5];
1 - 2 - 3 + 4 + 5 = 5 (YES) we have an expression to get x
solution :
for every number we have two options either addd numer or substract number
v = [1,2,3];
n = 3 , x = 5;
                   (1)
                 /     \
          (1+2)       (1-2)
          /    \       /    \
    (1+2+3)  (1+2-3)  (1-2+3)  (1-2-3)

  code is :
  /////////////////////////////////////////////////////////////////////////
  void recursion(int i , vector<ll> v , int sum , bool &flag,int n,int x){
    if(i==n){
        if(sum==x){
            flag = true;
        }
        return ;
    }
    recursion(i+1 ,v,sum+v[i],flag ,n ,x);
    recursion(i+1 ,v,sum-v[i],flag ,n ,x);
}
void solve() {
    ll n , x;
    cin>>n>>x;
    vector<ll> v(n);
    for(int i=0;i<n;i++) cin>>v[i];
    ll sum = v[0];
    bool flag = false;
    recursion(1,v ,sum , flag, n,x);
    if(flag){
        cout<<"YES"<<endl;
    }
    else{
        cout<<"NO"<<endl;
    }
}
/////////////////----------O/1 knapsack-------------//////////

You have N items, each with a weight wᵢ and value vᵢ. You have a bag that can carry up to W weight.

Choose items to put in the bag so that their total value is maximum, without exceeding W.

Solve using recursion.
Input:
4 10  
4 60  
3 50  
5 70  
2 30  

Output:
120
Best choice: Pick items (3,5,2) → Total Weight = 10, Total Value = 120.
N = 3, W = 10
Weights:  [4, 3, 5]
Values:   [60, 50, 70]
recustion tree: not take / take
                        (i=2, W=10)
                  /                    \
        (i=1, W=10)                   (i=1, W=5)  ← Took item 2 (wt=5val=70)
        /          \                    /          \
    (i=0, W=10)     (i=0, W=7)       (i=0, W=5)    (i=0, W=2)
    /       \        /      \         /      \       /     \
(60, 4)  (0, 10) (60, 4)   (0, 7)   (0, 5) (0, 2)  (0, 2)  (0, 2)
code: 
int recursion(int i , int w  , vector<int> val , vector<int> wt){
    if(i==0){
        if(wt[i]<=w) return val[i];
        else return 0;
    }
    int nottake = 0+recursion(i-1 , w , val , wt);
    int take = INT_MIN;
    if(wt[i]<=w){
        take = val[i]+recursion(i-1 , w-wt[i] , val , wt);
    }
    return max(nottake, take);
}
void solve() {
   int n , w;
   cin>>n>>w;
   vector<int> val(n);
   vector<int> wt(n);
   for(int i =0 ;i<n;i++){
        int x , y;
        cin>>x>>y;
        wt[i] = x;
        val[i] = y;
   }
   cout<<recursion(n-1 , w , val , wt);
}