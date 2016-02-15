# RED_SOCIAL

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='TRADITIONAL,ALLOW_INVALID_DATES';

CREATE SCHEMA IF NOT EXISTS `Red Social` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci ;
USE `Red Social` ;

-- -----------------------------------------------------
-- Table `Red Social`.`Pais`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Red Social`.`Pais` (
  `id_Pais` INT NOT NULL,
  `Nombre` VARCHAR(45) NULL,
  PRIMARY KEY (`id_Pais`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Red Social`.`Ciudad`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Red Social`.`Ciudad` (
  `id_Ciudad` INT NOT NULL,
  `Nombre` VARCHAR(45) NULL,
  `Pais_id_Pais` INT NOT NULL,
  PRIMARY KEY (`id_Ciudad`),
  INDEX `fk_Ciudad_Pais1_idx` (`Pais_id_Pais` ASC),
  CONSTRAINT `fk_Ciudad_Pais1`
    FOREIGN KEY (`Pais_id_Pais`)
    REFERENCES `Red Social`.`Pais` (`id_Pais`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Red Social`.`Municipio`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Red Social`.`Municipio` (
  `Id_Municipio` INT NOT NULL,
  `Nombre` VARCHAR(45) NULL,
  `Ciudad_id_Ciudad` INT NOT NULL,
  PRIMARY KEY (`Id_Municipio`),
  INDEX `fk_Municipio_Ciudad1_idx` (`Ciudad_id_Ciudad` ASC),
  CONSTRAINT `fk_Municipio_Ciudad1`
    FOREIGN KEY (`Ciudad_id_Ciudad`)
    REFERENCES `Red Social`.`Ciudad` (`id_Ciudad`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Red Social`.`Direccion`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Red Social`.`Direccion` (
  `id_Direccion` INT NOT NULL,
  `Nombre_Calle` VARCHAR(45) NULL,
  `Numero` VARCHAR(45) NULL,
  `Colonia` VARCHAR(45) NULL,
  `Codigo_Postal` INT NULL,
  `Municipio_Id_Municipio` INT NOT NULL,
  PRIMARY KEY (`id_Direccion`),
  INDEX `fk_Direccion_Municipio1_idx` (`Municipio_Id_Municipio` ASC),
  CONSTRAINT `fk_Direccion_Municipio1`
    FOREIGN KEY (`Municipio_Id_Municipio`)
    REFERENCES `Red Social`.`Municipio` (`Id_Municipio`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Red Social`.`Matricula`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Red Social`.`Matricula` (
  `id_Matricula` INT NOT NULL,
  `Matricula` VARCHAR(45) NULL,
  `Nombre` VARCHAR(45) NULL,
  PRIMARY KEY (`id_Matricula`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Red Social`.`Egresados`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Red Social`.`Egresados` (
  `Generacion` VARCHAR(10) NULL,
  `Carrera` VARCHAR(45) NULL,
  `Telefono` VARCHAR(45) NULL,
  `Fecha` VARCHAR(45) NULL,
  `Foto` VARCHAR(45) NULL,
  `Registro_Nickname` INT NOT NULL,
  `Direccion_id_Direccion` INT NOT NULL,
  `Matricula_id_Matricula` INT NOT NULL,
  PRIMARY KEY (`Registro_Nickname`),
  INDEX `fk_Egresados_Direccion1_idx` (`Direccion_id_Direccion` ASC),
  INDEX `fk_Egresados_Matricula1_idx` (`Matricula_id_Matricula` ASC),
  CONSTRAINT `fk_Egresados_Direccion1`
    FOREIGN KEY (`Direccion_id_Direccion`)
    REFERENCES `Red Social`.`Direccion` (`id_Direccion`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Egresados_Matricula1`
    FOREIGN KEY (`Matricula_id_Matricula`)
    REFERENCES `Red Social`.`Matricula` (`id_Matricula`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Red Social`.`TrabajoActual`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Red Social`.`TrabajoActual` (
  `id_trabajoActual` INT NOT NULL,
  `nombreEmpresa` VARCHAR(45) NULL,
  `direccionEmpresa` VARCHAR(45) NULL,
  `cargo` VARCHAR(45) NULL,
  `Horario` VARCHAR(45) NULL,
  `Egresados_Registro_Nickname` INT NOT NULL,
  `Egresados_Direccion_id_Direccion` INT NOT NULL,
  PRIMARY KEY (`id_trabajoActual`),
  INDEX `fk_TrabajoActual_Egresados1_idx` (`Egresados_Registro_Nickname` ASC, `Egresados_Direccion_id_Direccion` ASC),
  CONSTRAINT `fk_TrabajoActual_Egresados1`
    FOREIGN KEY (`Egresados_Registro_Nickname`)
    REFERENCES `Red Social`.`Egresados` (`Registro_Nickname`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Red Social`.`Oferta Academica`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Red Social`.`Oferta Academica` (
  `id_Oferta Academica` INT NOT NULL,
  `Becas_id_Becas` INT NOT NULL,
  PRIMARY KEY (`id_Oferta Academica`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Red Social`.`Registro`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Red Social`.`Registro` (
  `Nickname` INT NOT NULL,
  `Nombre(s)` VARCHAR(45) NULL,
  `Apellido_Pa` VARCHAR(45) NULL,
  `Apellido_Ma` VARCHAR(45) NULL,
  `E-mail` VARCHAR(45) NULL,
  `Password` VARCHAR(45) NULL,
  `Egresados_Registro_Nickname` INT NOT NULL,
  PRIMARY KEY (`Nickname`),
  INDEX `fk_Registro_Egresados1_idx` (`Egresados_Registro_Nickname` ASC),
  CONSTRAINT `fk_Registro_Egresados1`
    FOREIGN KEY (`Egresados_Registro_Nickname`)
    REFERENCES `Red Social`.`Egresados` (`Registro_Nickname`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Red Social`.`Detalle_Estudio`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Red Social`.`Detalle_Estudio` (
  `id_DetalleEstudio` INT NOT NULL,
  `Nivel de estudio` VARCHAR(45) NULL,
  `Universidad` VARCHAR(45) NULL,
  PRIMARY KEY (`id_DetalleEstudio`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Red Social`.`Amigos`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Red Social`.`Amigos` (
  `idAmigos` INT NOT NULL,
  `agregar` VARCHAR(45) NOT NULL,
  PRIMARY KEY (`idAmigos`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Red Social`.`Publicaciones`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Red Social`.`Publicaciones` (
  `idPublicaciones` INT NOT NULL,
  `Texto` VARCHAR(300) NOT NULL,
  `Imagenes` VARCHAR(45) NULL,
  `Amigos_idAmigos` INT NOT NULL,
  PRIMARY KEY (`idPublicaciones`),
  INDEX `fk_Publicaciones_Amigos1_idx` (`Amigos_idAmigos` ASC),
  CONSTRAINT `fk_Publicaciones_Amigos1`
    FOREIGN KEY (`Amigos_idAmigos`)
    REFERENCES `Red Social`.`Amigos` (`idAmigos`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Red Social`.`Chat`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Red Social`.`Chat` (
  `idMensaje` INT NOT NULL,
  `Texto` VARCHAR(500) NULL,
  `Imagen` VARCHAR(45) NULL,
  PRIMARY KEY (`idMensaje`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Red Social`.`Amigos_has_Egresados`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Red Social`.`Amigos_has_Egresados` (
  `Amigos_idAmigos` INT NOT NULL,
  `Egresados_Registro_Nickname` INT NOT NULL,
  PRIMARY KEY (`Amigos_idAmigos`, `Egresados_Registro_Nickname`),
  INDEX `fk_Amigos_has_Egresados_Egresados1_idx` (`Egresados_Registro_Nickname` ASC),
  INDEX `fk_Amigos_has_Egresados_Amigos1_idx` (`Amigos_idAmigos` ASC),
  CONSTRAINT `fk_Amigos_has_Egresados_Amigos1`
    FOREIGN KEY (`Amigos_idAmigos`)
    REFERENCES `Red Social`.`Amigos` (`idAmigos`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Amigos_has_Egresados_Egresados1`
    FOREIGN KEY (`Egresados_Registro_Nickname`)
    REFERENCES `Red Social`.`Egresados` (`Registro_Nickname`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Red Social`.`Egresados_has_Oferta Academica`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Red Social`.`Egresados_has_Oferta Academica` (
  `Egresados_Registro_Nickname` INT NOT NULL,
  `Oferta Academica_id_Oferta Academica` INT NOT NULL,
  PRIMARY KEY (`Egresados_Registro_Nickname`, `Oferta Academica_id_Oferta Academica`),
  INDEX `fk_Egresados_has_Oferta Academica_Oferta Academica1_idx` (`Oferta Academica_id_Oferta Academica` ASC),
  INDEX `fk_Egresados_has_Oferta Academica_Egresados1_idx` (`Egresados_Registro_Nickname` ASC),
  CONSTRAINT `fk_Egresados_has_Oferta Academica_Egresados1`
    FOREIGN KEY (`Egresados_Registro_Nickname`)
    REFERENCES `Red Social`.`Egresados` (`Registro_Nickname`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Egresados_has_Oferta Academica_Oferta Academica1`
    FOREIGN KEY (`Oferta Academica_id_Oferta Academica`)
    REFERENCES `Red Social`.`Oferta Academica` (`id_Oferta Academica`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Red Social`.`Intereses`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Red Social`.`Intereses` (
  `id_Intereses` INT NOT NULL,
  `Musica` VARCHAR(45) NULL,
  `Religion` VARCHAR(45) NULL,
  `Libros` VARCHAR(45) NULL,
  `Peliculas` VARCHAR(45) NULL,
  `Deportes` VARCHAR(45) NULL,
  PRIMARY KEY (`id_Intereses`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Red Social`.`Egresados_has_Intereses`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Red Social`.`Egresados_has_Intereses` (
  `Egresados_Registro_Nickname` INT NOT NULL,
  `Intereses_id_Intereses` INT NOT NULL,
  PRIMARY KEY (`Egresados_Registro_Nickname`, `Intereses_id_Intereses`),
  INDEX `fk_Egresados_has_Intereses_Intereses1_idx` (`Intereses_id_Intereses` ASC),
  INDEX `fk_Egresados_has_Intereses_Egresados1_idx` (`Egresados_Registro_Nickname` ASC),
  CONSTRAINT `fk_Egresados_has_Intereses_Egresados1`
    FOREIGN KEY (`Egresados_Registro_Nickname`)
    REFERENCES `Red Social`.`Egresados` (`Registro_Nickname`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Egresados_has_Intereses_Intereses1`
    FOREIGN KEY (`Intereses_id_Intereses`)
    REFERENCES `Red Social`.`Intereses` (`id_Intereses`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Red Social`.`Amigos_has_Chat`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Red Social`.`Amigos_has_Chat` (
  `Amigos_idAmigos` INT NOT NULL,
  `Chat_idMensaje` INT NOT NULL,
  PRIMARY KEY (`Amigos_idAmigos`, `Chat_idMensaje`),
  INDEX `fk_Amigos_has_Chat_Chat1_idx` (`Chat_idMensaje` ASC),
  INDEX `fk_Amigos_has_Chat_Amigos1_idx` (`Amigos_idAmigos` ASC),
  CONSTRAINT `fk_Amigos_has_Chat_Amigos1`
    FOREIGN KEY (`Amigos_idAmigos`)
    REFERENCES `Red Social`.`Amigos` (`idAmigos`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Amigos_has_Chat_Chat1`
    FOREIGN KEY (`Chat_idMensaje`)
    REFERENCES `Red Social`.`Chat` (`idMensaje`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Red Social`.`Status`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Red Social`.`Status` (
  `id_Status` INT NOT NULL,
  `Descripcion` VARCHAR(45) NULL,
  PRIMARY KEY (`id_Status`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Red Social`.`Notificaciones`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Red Social`.`Notificaciones` (
  `id_Notificaciones` INT NOT NULL,
  `Egresados_Registro_Nickname` INT NOT NULL,
  PRIMARY KEY (`id_Notificaciones`),
  INDEX `fk_Notificaciones_Egresados1_idx` (`Egresados_Registro_Nickname` ASC),
  CONSTRAINT `fk_Notificaciones_Egresados1`
    FOREIGN KEY (`Egresados_Registro_Nickname`)
    REFERENCES `Red Social`.`Egresados` (`Registro_Nickname`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Red Social`.`Solicitudes`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Red Social`.`Solicitudes` (
  `id_Solicitudes` INT NOT NULL,
  `Buscar` VARCHAR(45) NULL,
  `Enviar_solicitud` VARCHAR(45) NULL,
  `Aceptar_solicitud` VARCHAR(45) NULL,
  `Eliminar_solicitud` VARCHAR(45) NULL,
  PRIMARY KEY (`id_Solicitudes`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Red Social`.`Privacidad`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Red Social`.`Privacidad` (
  `id_Privacidad` INT NOT NULL,
  `Publico` VARCHAR(45) NULL,
  `Solo_amigos` VARCHAR(45) NULL,
  `Amigos_de_amigos` VARCHAR(45) NULL,
  `Solo_yo` VARCHAR(45) NULL,
  PRIMARY KEY (`id_Privacidad`))
ENGINE = InnoDB;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;
