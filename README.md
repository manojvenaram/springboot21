##  DemoApplication.java
```
package com.example.demo;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.stereotype.Component;

@SpringBootApplication
public class DemoApplication {

	public static void main(String[] args) {
		SpringApplication.run(DemoApplication.class, args);
	}
}

// Laptop Bean
@Component
class Laptop {
	private HardDisk hardDisk;
	private Battery battery;

	@Autowired
	public Laptop(HardDisk hardDisk, Battery battery) {
		this.hardDisk = hardDisk;
		this.battery = battery;
	}

	public HardDisk getHardDisk() {
		return hardDisk;
	}

	public Battery getBattery() {
		return battery;
	}
}

// HardDisk Bean
@Component
class HardDisk {
	public String readData() {
		return "Reading data from hard disk...";
	}
}

// Battery Bean
@Component
class Battery {
	public String checkChargeLevel() {
		return "Battery charge level: 75%";
	}
}

// Controller
@RestController
class MyController {
	@Autowired
	private Laptop laptop;

	@GetMapping
	public String test() {
		StringBuilder output = new StringBuilder();
		output.append("Laptop powered on.<br>");
		output.append(laptop.getHardDisk().readData()).append("<br>");
		output.append(laptop.getBattery().checkChargeLevel()).append("<br>");

		return output.toString();
	}
}
```
## Output:
![image](https://github.com/user-attachments/assets/4c215331-45ef-4213-9578-75ae5719bf5f)
