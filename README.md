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
AUTO_INCREMENT = 24
DEFAULT CHARACTER SET = utf8;


-- -----------------------------------------------------
-- Table `flexgram`.`users`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `flexgram`.`users` (
  `id` INT(11) NOT NULL AUTO_INCREMENT,
  `firstname` VARCHAR(30) NOT NULL,
  `lastname` VARCHAR(30) NOT NULL,
  `email` VARCHAR(100) NOT NULL,
  `phonenumber` VARCHAR(15) NOT NULL,
  `username` VARCHAR(30) NOT NULL,
  `password` VARCHAR(1000) NOT NULL,
  `macros_id` INT(11) NOT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_users_macros_idx` (`macros_id` ASC),
  CONSTRAINT `fk_users_macros`
    FOREIGN KEY (`macros_id`)
    REFERENCES `flexgram`.`macros` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB
AUTO_INCREMENT = 21
DEFAULT CHARACTER SET = utf8;


-- -----------------------------------------------------
-- Table `flexgram`.`foods`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `flexgram`.`foods` (
  `id` INT(11) NOT NULL AUTO_INCREMENT,
  `users_id` INT(11) NOT NULL,
  `foodName` VARCHAR(150) NOT NULL,
  `calories` INT(10) NOT NULL,
  `protein` INT(10) NOT NULL,
  `fats` INT(10) NOT NULL,
  `carbohydrates` INT(10) NOT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_foods_users1_idx` (`users_id` ASC),
  CONSTRAINT `fk_foods_users1`
    FOREIGN KEY (`users_id`)
    REFERENCES `flexgram`.`users` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB
AUTO_INCREMENT = 5
DEFAULT CHARACTER SET = utf8;


-- -----------------------------------------------------
-- Table `flexgram`.`posts`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `flexgram`.`posts` (
  `id` INT(11) NOT NULL AUTO_INCREMENT,
  `users_id` INT(11) NOT NULL,
  `postType` VARCHAR(50) NOT NULL,
  `username` VARCHAR(50) NOT NULL,
  `likes` INT(15) NOT NULL,
  `image` TEXT NOT NULL,
  `video` TEXT NOT NULL,
  `title` VARCHAR(200) NOT NULL,
  `description` TEXT NOT NULL,
  `ingredients` TEXT NOT NULL,
  `instructions` TEXT NOT NULL,
  `calories` INT(10) NOT NULL,
  `protein` INT(10) NOT NULL,
  `fats` INT(10) NOT NULL,
  `carbohydrates` INT(10) NOT NULL,
  `servings` INT(10) NOT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_recipeposts_users1_idx` (`users_id` ASC),
  CONSTRAINT `fk_recipeposts_users1`
    FOREIGN KEY (`users_id`)
    REFERENCES `flexgram`.`users` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB
AUTO_INCREMENT = 41
DEFAULT CHARACTER SET = utf8;


-- -----------------------------------------------------
-- Table `flexgram`.`user_likedposts`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `flexgram`.`user_likedposts` (
  `id` INT(11) NOT NULL AUTO_INCREMENT,
  `posts_id` INT(11) NOT NULL,
  `likedBy_UserId` INT(11) NOT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_user_likes_posts1_idx` (`posts_id` ASC),
  CONSTRAINT `fk_user_likes_posts1`
    FOREIGN KEY (`posts_id`)
    REFERENCES `flexgram`.`posts` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB
AUTO_INCREMENT = 23
DEFAULT CHARACTER SET = utf8;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;

