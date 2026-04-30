package com.myapp;

import org.junit.Test;
import static org.junit.Assert.*;

public class CalculatorTest {

	Calculator calc = new Calculator();

	@Test
	public void testAdd(){
		assertEquals(8, calc.add(5, 3));
	}
	@Test
	public void testSubstract(){
		assertEquals(8, calc.subtract(10, 2));
	}
	@Test
	public void testMultiply(){
		assertEquals(15, calc.multiply(3, 5));
	}

	@Test
	public void testDivide() {
        	assertEquals(5.0, calc.divide(15, 3), 0.001);
    	}

	@Test(expected = IllegalArgumentException.class)
	public void testDivideByZero() {
		calc.divide(10, 0);
	}
	
	@Test
	public void testAddNegative() {
		assertEquals(-2, calc.add(-5, 3));
	}
	
	@Test
	public void testSubtractNegative() {
		assertEquals(-8, calc.subtract(-5, 3));
	}
	
	@Test
	public void testMultiplyNegative() {
		assertEquals(15, calc.multiply(-5, -3));
	}
	
	@Test
	public void testDivideNegative() {
		assertEquals(5, calc.divide(-15, -3));
	}
}

