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

    System.setProperty("webdriver.chrome.driver", "C:\\app\\chromedriver_win32\\chromedriver.exe");  
    WebDriver d = new ChromeDriver();      
   
JavascriptExecutor  js = (JavascriptExecutor) d;
d.manage().window().maximize();

d.get("https://groceries.morrisons.com/browse/fresh-176739/milk-eggs-butter-176763");
d.findElement(By.xpath("/html/body/div[1]/div[1]/div[4]/div/button")).click();
List<WebElement> img = d.findElements(By.xpath("//ul[@class='fops fops-regular fops-shelf']/li"));
int im = img.size();
System.out.println("Total size : " +im);
int j=1;

for (int i=1; i<=im; i++) {

d.get("https://groceries.morrisons.com/browse/fresh-176739/milk-eggs-butter-176763");

Thread.sleep(7000);
WebElement a = d.findElement(By.xpath("/html/body/div[1]/div[1]/div[3]/div[2]/div[2]/ul/li["+ i +"]"));
js.executeScript("arguments[0].scrollIntoView();",a);
a.click();
Thread.sleep(4000);
WebElement b = d.findElement(By.xpath("//div[@id='react-view']/div/div[3]/article/section[1]/div/div/div[1]/img"));
//System.out.println(a);  
String fi = b.getAttribute("src");
d.get(fi);
WebElement scr = d.findElement(By.xpath("/html/body/img"));  
 ss(scr,"image"+j);  
 j++;    
 System.out.println(fi);
 
//  d.navigate().back();
//  
//  Thread.sleep(1000);
//  
//  d.navigate().back();
//  
//  Thread.sleep(1000);
 
//  "+ i +"  
}

d.quit();
    }    
   
   
    public static void ss(WebElement element, String Name) throws IOException
   
    {
   
    File f = element.getScreenshotAs(OutputType.FILE);
       
FileUtils.copyFile(f, new File("C:\\app\\Fresh\\milk-eggs-butter\\"+ Name +".jpg"));
   
    }
   
}