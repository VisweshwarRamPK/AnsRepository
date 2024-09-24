**2) WRITE A BACKGROUND JOB IN JAVA AND SCHEDULE TO RUN**

**I) DEFINITION:**

A background job in Java can be scheduled using Spring Boot’s `@Scheduled` annotation, allowing you to execute tasks periodically or according to a cron schedule.

**II) Steps to Create a Background Job with Cron Scheduling in Spring Boot:**

**Step 1: Setting Up Dependencies**

Ensure the following dependencies are added in your `pom.xml`:



* `spring-boot-starter`
* `spring-boot-starter-web`

These are required to set up a basic Spring Boot application.

**Step 2: Enable Scheduling in Spring Boot**

Add the `@EnableScheduling` annotation in your main application class to enable scheduling functionality.

import org.springframework.boot.SpringApplication;

import org.springframework.boot.autoconfigure.SpringBootApplication;

import org.springframework.scheduling.annotation.EnableScheduling;

@SpringBootApplication

@EnableScheduling

public class BackgroundJobApplication {

    public static void main(String[] args) {

        SpringApplication.run(BackgroundJobApplication.class, args);

    }

}


##### **Step 3: Create a Background Job in a Class**

Use the `@Scheduled` annotation with a cron expression to define when the job should run.

import org.springframework.scheduling.annotation.Scheduled;

import org.springframework.stereotype.Component;

@Component

public class MyBackgroundJob {

    // This method will run every minute

    @Scheduled(cron = "0 * * * * ?")

    public void runJob() {

        System.out.println("Background job is running...");

        // Actual logic, like sending emails or processing data

    }

}

**IV)DIFFERENT SCHEDULING OPTIONS:**

**Fixed Rate: **Runs the job at a fixed interval (e.g., every 10 seconds).

**@Scheduled(fixedRate = 10000)**

**Fixed Delay: **Runs the job after a fixed delay, waiting for the current job to finish (e.g., 10 seconds delay).

**@Scheduled(fixedDelay = 10000)**

**Cron Expression: **Schedules the job based on cron expressions for advanced scheduling, such as running the job every minute.

**@Scheduled(cron = "0 * * * * ?")**

**V)UNDERSTANDING CRON EXPRESSION:**

**┌───────────── second (0-59)**

**│ ┌───────────── minute (0-59)**

**│ │ ┌───────────── hour (0-23)**

**│ │ │ ┌───────────── day of the month (1-31)**

**│ │ │ │ ┌───────────── month (1-12)**

**│ │ │ │ │ ┌───────────── day of the week (0-7) (Sunday-Saturday)**

*** * * * * ?**
