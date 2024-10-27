# FlexGram-DDL-Script
-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------
-- -----------------------------------------------------
-- Schema flexgram
-- -----------------------------------------------------

-- -----------------------------------------------------
-- Schema flexgram
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `flexgram` DEFAULT CHARACTER SET utf8 ;
USE `flexgram` ;

-- -----------------------------------------------------
-- Table `flexgram`.`macros`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `flexgram`.`macros` (
  `id` INT(11) NOT NULL AUTO_INCREMENT,
  `calories` INT(10) NOT NULL,
  `protein` INT(10) NOT NULL,
  `fats` INT(10) NOT NULL,
  `carbohydrates` INT(10) NOT NULL,
  PRIMARY KEY (`id`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;


-- -----------------------------------------------------
-- Table `flexgram`.`users`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `flexgram`.`users` (
  `id` INT(11) NOT NULL AUTO_INCREMENT,
  `firstname` VARCHAR(30) NOT NULL,
  `lastname` VARCHAR(30) NOT NULL,
  `email` VARCHAR(100) NOT NULL,
  `phonenumber` INT(11) NOT NULL,
  `username` VARCHAR(30) NOT NULL,
  `password` VARCHAR(35) NOT NULL,
  `macros_id` INT(11) NOT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_users_macros_idx` (`macros_id` ASC) VISIBLE,
  CONSTRAINT `fk_users_macros`
    FOREIGN KEY (`macros_id`)
    REFERENCES `flexgram`.`macros` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;


-- -----------------------------------------------------
-- Table `flexgram`.`foods`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `flexgram`.`foods` (
  `id` INT(11) NOT NULL AUTO_INCREMENT,
  `users_id` INT(11) NOT NULL,
  `foodName` INT(100) NOT NULL,
  `calories` INT(10) NOT NULL,
  `protein` INT(10) NOT NULL,
  `fats` INT(10) NOT NULL,
  `carbohydrates` INT(10) NOT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_foods_users1_idx` (`users_id` ASC) VISIBLE,
  CONSTRAINT `fk_foods_users1`
    FOREIGN KEY (`users_id`)
    REFERENCES `flexgram`.`users` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;


-- -----------------------------------------------------
-- Table `flexgram`.`recipeposts`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `flexgram`.`recipeposts` (
  `id` INT(11) NOT NULL AUTO_INCREMENT,
  `users_id` INT(11) NOT NULL,
  `userName` VARCHAR(50) NOT NULL,
  `likes` INT(15) NOT NULL,
  `image` TEXT NOT NULL,
  `recipeName` VARCHAR(200) NOT NULL,
  `description` TEXT NOT NULL,
  `ingredients` TEXT NOT NULL,
  `instructions` TEXT NOT NULL,
  `calories` INT(10) NOT NULL,
  `protein` INT(10) NOT NULL,
  `fats` INT(10) NOT NULL,
  `carbohydrates` INT(10) NOT NULL,
  `servings` INT(10) NOT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_recipeposts_users1_idx` (`users_id` ASC) VISIBLE,
  CONSTRAINT `fk_recipeposts_users1`
    FOREIGN KEY (`users_id`)
    REFERENCES `flexgram`.`users` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;


-- -----------------------------------------------------
-- Table `flexgram`.`videoposts`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `flexgram`.`videoposts` (
  `id` INT(11) NOT NULL AUTO_INCREMENT,
  `users_id` INT(11) NOT NULL,
  `userName` VARCHAR(50) NOT NULL,
  `likes` INT(15) NOT NULL,
  `video` TEXT NOT NULL,
  `title` VARCHAR(150) NOT NULL,
  `description` TEXT NOT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_videoposts_users1_idx` (`users_id` ASC) VISIBLE,
  CONSTRAINT `fk_videoposts_users1`
    FOREIGN KEY (`users_id`)
    REFERENCES `flexgram`.`users` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;
