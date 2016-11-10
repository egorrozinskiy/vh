#include <iostream>
#include <vector>
template <class T>
class CircularBuffer
{
public:

    CircularBuffer( int size )
    {
        head = tail = length = 0;
        bufferSize = size;
        arr = new int[bufferSize];
    }

    ~CircularBuffer()
    {
        delete[] arr;
    }

    // Добавить элемент
    void put( const int & value )
    {
        if ( tail == bufferSize )
        {
            tail = 0;
        }

        arr[tail] = value;
        ++tail;
        ++length;
    }


    // Извлечь последний элемент
    T & pop()
    {

        int & elem = arr[head];
        ++head;
        --length;
        if ( head == bufferSize ) {
            head = 0;
        }
        return elem;
    }

    // Кол-во элементов в буфере
    size_t size() const
    {
        return length;
    }

    // Ёмкость буфера
    size_t capacity() const
    {
        return bufferSize;
    }

    T operator[](const int &i)
    {
        return arr[i];
    }

    void printBuffer()
    {
        std::cout << head << " " << tail << std::endl;
        for(int i=0;i<length;i++)
        {
            std::cout << arr[i] <<";";
        }
        std::cout << std::endl;
    }




private:
    int * arr;             // массив-буфер
    int bufferSize;        // размер буфера
    int length;            // кол-во элементов в буффере
    int head;              // индекс первого элемента
    int tail;              // индекс последнего элемента
};


int main()
{
    CircularBuffer<int>buf(3);
    buf.printBuffer();
    for( int i = 0; i < 10; ++i )
    {
        buf.put( i * 2 );
        if ( buf.size() == buf.capacity() ) {
            std::cout << "---------------" << std::endl;
            while( buf.size() ) {
                std::cout << buf.pop() << std::endl;
            }
        }

    }

    std::cout << "---------------" << std::endl;
    while( buf.size() ) {
        std::cout << buf.pop() << std::endl;
    }
    return 0;
}
