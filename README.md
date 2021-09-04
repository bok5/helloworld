import java.io.*;
import java.util.Random;
import java.util.Scanner;

public class Main
{
    public static void main(String[] args) throws FileNotFoundException, IOException
    {
        Random r=new Random();
        Scanner in=new Scanner(System.in);
        System.out.print("请输入题目的个数：");  //输入所需题目的数量
        int N=in.nextInt();
        String op1,op2; //运算符
        int k1,k2,k3; //运算数
        int n; //运算符的个数
        int[] answer=new int[N];  //答案数组
        int i,j,w=0;
        String y;  //运算式
        OutputStream os1=new FileOutputStream("Exercises.txt");
        PrintWriter pw1=new PrintWriter(os1);
        OutputStream os2=new FileOutputStream("Answers.txt");
        PrintWriter pw2=new PrintWriter(os2);
        for(i=0;i<N;i++)
        {
            k1=r.nextInt(100); //第一个运算数
            k2=r.nextInt(100);  //第二个运算数
            n=r.nextInt(2);  //一个运算符或两个运算符
            do
            {
                if(n==0)
                {
                    op1=r.nextInt(2)==0?"+":"-";
                    y=(i+1)+". "+k1+op1+k2+"=";
                    answer[i]=op1=="+"?(k1+k2):(k1-k2);
                }
                else
                {
                    op1=r.nextInt(2)==0?"+":"-";
                    op2=r.nextInt(2)==0?"+":"-";
                    k3=r.nextInt(100);
                    y=(i+1)+". "+k1+op1+k2+op2+k3+"=";
                    int t=op1=="+"?(k1+k2):(k1-k2);
                    answer[i]=op2=="+"?(t+k3):(t-k3);
                }
                for(w=0;w<i;w++)
                {
                    if(answer[w]==answer[i])
                        break;
                }
            }while (w!=i);  //要求每道题的答案各不相同
            pw1.println(y);
            pw2.println((i+1)+". "+answer[i]);
        }
        pw1.close();
        pw2.close();
        os1.close();
        os2.close();
    }
}


