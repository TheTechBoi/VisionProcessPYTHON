/*----------------------------------------------------------------------------*/
/* Copyright (c) 2017-2018 FIRST. All Rights Reserved.                        */
/* Open Source Software - may be modified and shared by FRC teams. The code   */
/* must be accompanied by the FIRST BSD license file in the root directory of */
/* the project.                                                               */
/*----------------------------------------------------------------------------*/

package frc.robot;

import edu.wpi.first.wpilibj.IterativeRobot;
import edu.wpi.first.wpilibj.smartdashboard.SendableChooser;
import edu.wpi.first.wpilibj.smartdashboard.SmartDashboard;
import edu.wpi.first.wpilibj.drive.DifferentialDrive;
import com.ctre.phoenix.motorcontrol.can.WPI_VictorSPX;
import edu.wpi.first.wpilibj.Joystick;
import edu.wpi.first.wpilibj.SpeedControllerGroup;




/**
 * The VM is configured to automatically run this class, and to call the
 * functions corresponding to each mode, as described in the IterativeRobot
 * documentation. If you change the name of this class or the package after
 * creating this project, you must also update the build.gradle file in the
 * project.
 */

public class Robot extends IterativeRobot {

  boolean toggleOn = false;
  boolean togglePressed = false;

  public static WPI_VictorSPX sag1 = new WPI_VictorSPX(2);
  public static WPI_VictorSPX sag2 = new WPI_VictorSPX(10);

  public static WPI_VictorSPX sol1 = new WPI_VictorSPX(5);
  public static WPI_VictorSPX sol2 = new WPI_VictorSPX(6);
  //public static WPI_VictorSPX asonsor1 = new WPI_VictorSPX(9);
  //public static WPI_VictorSPX asonsor2 = new WPI_VictorSPX(1);

  public static Joystick stick = new Joystick(0);

  public static SpeedControllerGroup sag = new SpeedControllerGroup(sag1, sag2);
  public static SpeedControllerGroup sol = new SpeedControllerGroup(sol1, sol2);
  
  public static DifferentialDrive sdrive = new DifferentialDrive(sol, sag);
  //public static DifferentialDrive asonsorDrive= new DifferentialDrive(asonsor1, asonsor2)
 
  /**<
   * 
  	Spark m_frontLeft = new Spark(1);
	Spark m_rearLeft = new Spark(2);
	SpeedControllerGroup m_left = new SpeedControllerGroup(m_frontLeft, m_rearLeft);

	Spark m_frontRight = new Spark(3);
	Spark m_rearRight = new Spark(4);
	SpeedControllerGroup m_Right = new SpeedControllerGroup(m_frontRight, m_rearRight);
	DifferentialDrive m_drive = new DifferentialDrive(m_left, m_right);
   * 
   * 
   * 
   * 
   * 
   * 
   * 
   * 
   * This function is run when the robot is first started up and should be
   * used for any initialization code.
   */
  @Override
  public void robotInit() {
   }

  /**
   * This function is called every robot packet, no matter the mode. Use
   * this for items like diagnostics that you want ran during disabled,
   * autonomous, teleoperated and test.
   *
   * <p>This runs after the mode specific periodic functions, but before
   * LiveWindow and SmartDashboard integrated updating.
   */
  @Override
  public void robotPeriodic() {
  }

  /**
   * This autonomous (along with the chooser code above) shows how to select
   * between different autonomous modes using the dashboard. The sendable
   * chooser code works with the Java SmartDashboard. If you prefer the
   * LabVIEW Dashboard, remove all of the chooser code and uncomment the
   * getString line to get the auto name from the text box below the Gyro
   *
   * <p>You can add additional auto modes by adding additional comparisons to
   * the switch structure below with additional strings. If using the
   * SendableChooser make sure to add them to the chooser code above as well.
   */
  @Override
  public void autonomousInit() {
   
  }

  /**
   * This function is called periodically during autonomous.
   */
  @Override
  public void autonomousPeriodic() {
    /*asonsor1.set(0.1*(stick.getRawAxis(1) - stick.getRawAxis(5)));
    asonsor2.set(0.1*(stick.getRawAxis(1) - stick.getRawAxis(5)))  ;*/
    sdrive.tankDrive(stick.getRawAxis(1), stick.getRawAxis(5)); // r1-l1
   
  }

  /**
   * This function is   called periodically during operator control.
   */


  @Override
  public void teleopPeriodic() {

    double haz = 0.8; //button or buttonpressed
    //SmartDashboard.putBoolean("ardagay", stick.getRawButtonPressed(4)); //yavaslatma calısmayan kısım:
    if (stick.getRawButton(4) == true && stick.getRawButton(5) == false ) {
      haz = 0.6;

    } else if(stick.getRawButton(4) == false && stick.getRawButton(5) == true) {
      haz = 1;

    } else if(stick.getRawButton(4) == false && stick.getRawButton(5) == false){

      haz = 0.8;
    }
    
    sdrive.tankDrive(haz*stick.getRawAxis(1),  haz*stick.getRawAxis(5));

    }

  /*  public void updateToggle()
    {
        if(stick.getRawButton(1)){
            if(!togglePressed){
                toggleOn = !toggleOn;
                togglePressed = true;
            }
        }else{
            togglePressed = false;
        }
    }
    */
   









/*@Override
  public void teleopPeriodic() {
    SmartDashboard.putBoolean("ardagay", stick.getRawButtonPressed(4)); //yavaslatma
    if (stick.getRawButtonPressed(4)) {
      sdrive.tankDrive(0.4*stick.getRawAxis(1), 0.4*stick.getRawAxis(5));
    } else {
      sdrive.tankDrive(stick.getRawAxis(1), stick.getRawAxis(5));
    }
  }
*/





  /**
   * This function is called periodically during test mode.
   */
  @Override
  public void testPeriodic() {
  }
}
