package complete_prj;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.Assert;
import org.testng.ITestResult;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.Test;

import com.relevantcodes.extentreports.ExtentReports;
import com.relevantcodes.extentreports.LogStatus;

 public class scrrenShot {
	WebDriver driver;
	
	@Test
	public void capturescreenShot() throws Exception{
		
		System.setProperty("webdriver.chrome.driver", "E:\\browser\\chromedriver_win32\\chromedriver.exe");
		
		  ExtentReports logger = ExtentReports.get(scrrenShot.class);
			logger.init("E:\\report\\advanceReport\\advanceReport1.html", true);
			logger.startTest("Verify Page Titel");
		
		WebDriver driver =new ChromeDriver();
		logger.log(LogStatus.INFO, "Browser is up and running");
		driver.get("https://www.gmail.com");
		logger.log(LogStatus.INFO, "Application is up and running");
		String title=driver.getTitle();
		logger.log(LogStatus.INFO, "Title Captured");
		Assert.assertTrue(title.contains("Gmail"));
		logger.log(LogStatus.PASS, "Title is verified");
	    Utility.captureScreenShot(driver,"BrowserStarted");
	    Utility.captureScreenShot(driver,"TypeName");
		logger.log(LogStatus.PASS, "Title is verified");
	    driver.findElement(By.xpath("//*[@id='identifierId']")).sendKeys("");
	    logger.endTest();
	
	
	}
	
	
	@AfterMethod
	
	public void tearDown(ITestResult result) throws Exception{
		if(ITestResult.SUCCESS==result.getStatus())
		{
			Utility.captureScreenShot(driver, result.getName());
			
		}
		driver.quit();
	}
}
