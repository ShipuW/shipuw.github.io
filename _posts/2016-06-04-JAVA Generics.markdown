---
layout: post
title: JAVA Generics
date: 2016-06-04
excerpt_separator: <!--more-->
---
In JAVA, the default type of elements in a list is **Object**. So when we take out elements in the list, there may exists java.lang.ClassCastException situation. Then, the JAVA Generics are introduced in our program.


<!--more-->

# JAVA Generics #

Complie Error in Program:


	public class GenericTest {
	
	    public static void main(String[] args) {
	        /*
	        List list = new ArrayList();
	        list.add("qqyumidi");
	        list.add("corn");
	        list.add(100);
	        */
	
	        List<String> list = new ArrayList<String>();
	        list.add("qqyumidi");
	        list.add("corn");
	        //list.add(100);   //COMPILE ERROR
	
	        for (int i = 0; i < list.size(); i++) {
	            String name = list.get(i); // Get String Type
	            System.out.println("name:" + name);
	        }
	    }
	}



## What is JAVA Generics? ##

After Java SE 1.5, Generics is introduced to solve the random parameters. In List<E>, List<String> and List, List<E> is parameterized type. E in (formal) type parameter. String is actual type argument. List is raw type.


## List Interface ##

	public interface List<E> extends Collection<E> {

	    int size();
	
	    boolean isEmpty();
	
	    boolean contains(Object o);
	
	    Iterator<E> iterator();
	
	    Object[] toArray();
	
	    <T> T[] toArray(T[] a);
	
	    boolean add(E e);
	
	    boolean remove(Object o);
	
	    boolean containsAll(Collection<?> c);
	
	    boolean addAll(Collection<? extends E> c);
	
	    boolean addAll(int index, Collection<? extends E> c);
	
	    boolean removeAll(Collection<?> c);
	
	    boolean retainAll(Collection<?> c);
	
	    void clear();
	
	    boolean equals(Object o);
	
	    int hashCode();
	
	    E get(int index);
	
	    E set(int index, E element);
	
	    void add(int index, E element);
	
	    E remove(int index);
	
	    int indexOf(Object o);
	
	    int lastIndexOf(Object o);
	
	    ListIterator<E> listIterator();
	
	    ListIterator<E> listIterator(int index);
	
	    List<E> subList(int fromIndex, int toIndex);

	}

In the defination, E in <E> is formal parameter. Every E in this interface can receive actual parameter from external.

## Generic Interfaces, Classes, Methods ##

A simple defination.


	
	class Box<T> {
	
	    private T data;
	
	    public Box() {
	
	    }
	
	    public Box(T data) {
	        this.data = data;
	    }
	
	    public T getData() {
	        return data;
	    }

		public void showType() {
			System.out.println("Actual type:" + data.getClass().getName());
		}
	
	}

	public class GenericTest {
	
	    public static void main(String[] args) {
	
	        Box<String> name = new Box<String>("corn");
	        Box<Integer> age = new Box<Integer>(712);
			
			name.showType();	//java.lang.String
	        System.out.println("name class:" + name.getClass());      // com.test.Box
			
			age.showType();		//java.lang.Integer
	        System.out.println("age class:" + age.getClass());        // com.test.Box

	        System.out.println(name.getClass() == age.getClass());    // true
	
	    }
	
	}

We can notice a fact in this case. Although Generics types are seemingly to be different types in logic, they are actually same type.

## FOLLOW UP ##


***
