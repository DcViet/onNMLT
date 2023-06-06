# onNMLT
---
title: ABOUT PAGE
layout: template
filename: Ontap.md
--- 
#hk1 22-23 (12/11/2022)
câu 1:[3đ]: viết hàm nhận vào 3 tham số ngày tháng năm cho biết đó là ngày thứ mấy trong tuần.
*write a function that takes in 3 arguments the date of the year indicating what day of the week it is.*
***Hướng làm: nếu không sử dụng các hàm trong thư viện có sẵn (vd: hàm Datetime,..) 
có thể sử dụng công thức Zeller's Congruence***
**bài làm:** 
'''
using System;

public struct NgayThangNam
{
    public int Ngay;
    public int Thang;
    public int Nam;
}

public class Program
{
    public static void Main(string[] args)
    {
        NgayThangNam ngayThangNam;

        Console.WriteLine("Nhập ngày (1-31):");
        ngayThangNam.Ngay = int.Parse(Console.ReadLine());

        Console.WriteLine("Nhập tháng (1-12):");
        ngayThangNam.Thang = int.Parse(Console.ReadLine());

        Console.WriteLine("Nhập năm:");
        ngayThangNam.Nam = int.Parse(Console.ReadLine());

        int ngayTrongTuan = TimNgayTrongTuan(ngayThangNam);
        string thu = LayTenThu(ngayTrongTuan);

        Console.WriteLine($"Ngày {ngayThangNam.Ngay}/{ngayThangNam.Thang}/{ngayThangNam.Nam} là {thu}");
    }

    public static int TimNgayTrongTuan(NgayThangNam ngayThangNam)
    {
        int ngay = ngayThangNam.Ngay;
        int thang = ngayThangNam.Thang;
        int nam = ngayThangNam.Nam;

        if (thang < 3)
        {
            thang += 12;
            nam--;
        }

        int namThapKy = nam % 100;
        int theKy = nam / 100;

        int ngayTrongTuan = (ngay + 2 * thang + 3 * (thang + 1) / 5 + namThapKy + namThapKy / 4 - namThapKy / 100 + namThapKy / 400) % 7;

        return ngayTrongTuan + 1; // Chuyển về dạng 1 (thứ hai) đến 7 (Chủ nhật)
    }

    public static string LayTenThu(int ngayTrongTuan)
    {
        string[] tenThu = { "Chủ nhật", "Thứ hai", "Thứ ba", "Thứ tư", "Thứ năm", "Thứ sáu", "Thứ bảy" };
        return tenThu[ngayTrongTuan - 1];
    }
}

'''
/* khong su dung kieu du kieu struct */
'''
using System;

public class Program
{
    public static int TimThuNgay(int ngay, int thang, int nam)
    {
        if (thang < 3)
        {
            thang += 12;
            nam--;
        }

        int namThapKy = nam % 100;
        int theKy = nam / 100;

        int ngayTrongTuan = (ngay + 2 * thang + 3 * (thang + 1) / 5 + namThapKy + namThapKy / 4 - namThapKy / 100 + namThapKy / 400) % 7;

        return ngayTrongTuan + 1; // Chuyển về dạng 1 (thứ hai) đến 7 (Chủ nhật)
    }

    public static string LayTenThu(int ngayTrongTuan)
    {
        string[] tenThu = { "Chủ nhật", "Thứ hai", "Thứ ba", "Thứ tư", "Thứ năm", "Thứ sáu", "Thứ bảy" };
        return tenThu[ngayTrongTuan - 1];
    }

    public static void Main(string[] args)
    {
        Console.WriteLine("Nhập ngày (1-31):");
        int ngay = int.Parse(Console.ReadLine());

        Console.WriteLine("Nhập tháng (1-12):");
        int thang = int.Parse(Console.ReadLine());

        Console.WriteLine("Nhập năm:");
        int nam = int.Parse(Console.ReadLine());

        int ngayTrongTuan = TimThuNgay(ngay, thang, nam);
        string thu = LayTenThu(ngayTrongTuan);

        Console.WriteLine($"Ngày {ngay}/{thang}/{nam} là {thu}");
    }
}

'''
câu 2:4đ: viết hàm đếm số lần xuất hiện của phần tử nhỏ nhất trong mảng 1 chiều các số nguyên. 
vd: A:{1,2,10,3,1,9,1} -> số nhỏ nhất là 1 và xuất hiện 3 lần
'''
using System;

public class Program
{
    public static int DemSoNhoNhat(int[] arr)
    {
        int min = arr[0];
        int count = 0;

        foreach (int num in arr)
        {
            if (num < min)
            {
                min = num;
                count = 1;
            }
            else if (num == min)
            {
                count++;
            }
        }

        return count;
    }

    public static void Main(string[] args)
    {
        int[] array = { 1, 2, 10, 3, 1, 9, 1 };
        int soNhoNhatXuatHien = DemSoNhoNhat(array);
        Console.WriteLine($"Số lần xuất hiện của phần tử nhỏ nhất: {soNhoNhatXuatHien}");
    }
}

'''
câu 3:3đ: viết hàm tính trung bình cộng các số nguyên tố trong ma trận có các số nguyên. 
(số nguyên tố là số chỉ chia hết cho 1 và chính nó)
'''
using System;

public class Program
{
    public static bool IsPrime(int n)
    {
        if (n <= 1)
            return false;
        if (n == 2)
            return true;
        if (n % 2 == 0)
            return false;
        int sqrt_n = (int)Math.Sqrt(n) + 1;
        for (int divisor = 3; divisor < sqrt_n; divisor += 2)
        {
            if (n % divisor == 0)
                return false;
        }
        return true;
    }

    public static double AverageOfPrimes(int[,] matrix)
    {
        int primeSum = 0;
        int primeCount = 0;
        int rows = matrix.GetLength(0);
        int columns = matrix.GetLength(1);
        for (int row = 0; row < rows; row++)
        {
            for (int column = 0; column < columns; column++)
            {
                if (IsPrime(matrix[row, column]))
                {
                    primeSum += matrix[row, column];
                    primeCount++;
                }
            }
        }
        if (primeCount > 0)
        {
            double average = (double)primeSum / primeCount;
            return average;
        }
        else
        {
            return 0;
        }
    }

    public static void Main()
    {
        int[,] matrix = {
            { 1, 2, 3 },
            { 4, 5, 6 },
            { 7, 8, 9 }
        };

        double avg = AverageOfPrimes(matrix);
        Console.WriteLine(avg);
    }
}

'''
