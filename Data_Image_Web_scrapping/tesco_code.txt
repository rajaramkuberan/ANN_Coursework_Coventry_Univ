package Automation.Images;

import java.io.File;
import java.io.IOException;
import java.util.List;
import org.apache.commons.io.FileUtils;
import org.openqa.selenium.By;
import org.openqa.selenium.JavascriptExecutor;
//import org.openqa.selenium.JavascriptExecutor;
import org.openqa.selenium.OutputType;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;

public class App 
{

public static void main( String[] args ) throws InterruptedException, IOException
    {

    System.setProperty("webdriver.chrome.driver", "Data_Image_Web_scrapping\\chromedriver_win32\\chromedriver.exe");  
    WebDriver d = new ChromeDriver();      
   
JavascriptExecutor  js = (JavascriptExecutor) d;
d.manage().window().maximize();

d.get("https://www.tesco.com/groceries/en-GB/shop/fresh-food/fresh-soup-sandwiches-and-salad-pots/all");

Thread.sleep(7000);

d.findElement(By.xpath("//*[@id='sticky-bar-cookie-wrapper']/span/div/div/div[2]/form/button")).click();
List<WebElement> img = d.findElements(By.xpath("//*[@id='product-list']/div[2]/div[4]/div[2]/div/div/div/ul/li"));

int im = img.size();
   System.out.println("Total size : " +im);    
   int j = 1;
   

   

for(int x = 1; x<=13; x++) // x is the number of pages in each website
	
	

{
d.get("https://www.tesco.com/groceries/en-GB/shop/fresh-food/fresh-soup-sandwiches-and-salad-pots/all?page="+ x +"");

for (int i=1; i<=im; i++)

{
{

d.get("https://www.tesco.com/groceries/en-GB/shop/fresh-food/fresh-soup-sandwiches-and-salad-pots/all?page="+ x +"");



d.findElement(By.xpath("//*[@id='main']")).click();


WebElement  a = d.findElement(By.xpath("/html/body/div[1]/div/div/div[3]/div[1]/div/div[1]/div[1]/div[2]/div[4]/div[2]/div/div/div/ul/li["+ i +"]/div/div/div/div/a/div/img"));

js.executeScript("arguments[0].scrollIntoView();", a);

a.click();

Thread.sleep(3000);

WebElement b = d.findElement(By.xpath("/html/body/div[1]/div/div/div[3]/div[1]/div/div[1]/div[2]/div[2]/div/div[1]/div[1]/div/div[2]/span/div/div/img"));

String fi = b.getAttribute("src");

d.get(fi);

WebElement scr = d.findElement(By.xpath("/html/body/img"));

ss(scr,"Tesco"+j);

j++;  

System.out.println(fi);

}


}

}


d.close();
   }    
   
   
    public static void ss(WebElement element, String Name) throws IOException
   
    {
   
    File f = element.getScreenshotAs(OutputType.FILE);
       
FileUtils.copyFile(f, new File("F:\\Tesco\\"+ Name +".jpg"));
   
    }
  }
